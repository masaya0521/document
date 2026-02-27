# Rust の非同期ランタイムと言語間マルチスレッドモデル比較

- **日付**: 2026-02-27
- **カテゴリ**: Language / Runtime / Concurrency
- **前編**: [TypeScript 6.0/7.0 深掘り — Go 書き直しと言語ランタイムの並行性モデル](./typescript-7-go-rewrite-and-concurrency-models.md)

## 1. 概要

本ドキュメントは、2/20 の TypeScript 7.0 Go 書き直しに関する Deep Dive 記事の続編として、以下のトピックを深掘りしたものである：

- Rust (tokio) による非同期ランタイムのアーキテクチャと、大規模 Web アプリケーションでの活用パターン
- Node.js Worker Threads と Go/Rust の共有メモリモデルの根本的な違い
- DataLoader パターンの言語間比較
- バックエンド言語選択の判断基準

前回の記事では「I/O がボトルネックの場合、Go でも JavaScript でも性能差はほとんどない」と結論づけた。本稿では、**アプリケーション内でのデータ共有が必要な場面では明確な差が出る**という補足を加え、各言語の並行性モデルをより実践的な観点から比較する。

---

## 2. Rust (tokio) の非同期ランタイムアーキテクチャ

### プロセス・スレッド・タスクの関係

Rust の非同期ランタイム tokio は、1 プロセス内に複数の OS スレッドを立ち上げ、その上で軽量な非同期タスクを実行する。

```
┌─────────────── 1つのプロセス ──────────────────────┐
│                                                    │
│  tokio ランタイム（プロセス起動時に初期化）           │
│  ├── OS スレッド 1 [ローカルキュー + Event Loop]     │
│  ├── OS スレッド 2 [ローカルキュー + Event Loop]     │
│  ├── OS スレッド 3 [ローカルキュー + Event Loop]     │
│  └── OS スレッド 4 [ローカルキュー + Event Loop]     │
│           ↑                                        │
│     デフォルトで CPU コア数ぶん生成される              │
│                                                    │
│  共有メモリ空間（全スレッドからアクセス可能）          │
│  ├── AppState（キャッシュ、DB プール、Redis 等）     │
│  └── リクエストごとの共有状態                        │
└────────────────────────────────────────────────────┘
```

重要なのは、**「振り分け役の専用スレッド」は存在しない**という点。各スレッドが対等にランタイムの機能を内蔵しており、中央の司令塔はいない。

```
❌ 間違ったイメージ:
  [ランタイム専用スレッド]  ← 司令塔が1つあって
       ↓    ↓    ↓
  [Thread1] [Thread2] [Thread3]  ← ワーカーに仕事を配る

✅ 正しいイメージ:
  [Thread 1]          [Thread 2]          [Thread 3]
   ランタイム機能を      ランタイム機能を      ランタイム機能を
   内蔵している          内蔵している          内蔵している
   ┌────────────┐    ┌────────────┐    ┌────────────┐
   │ローカルキュー│    │ローカルキュー│    │ローカルキュー│
   │ [タスクA]   │    │ [タスクB]   │    │ [タスクC]   │
   │ [タスクD]   │    │            │    │ [タスクE]   │
   └────────────┘    └────────────┘    └────────────┘
              ↑              ↑              ↑
              └──── グローバルキュー ─────────┘
                    [タスクF, タスクG]
```

### ワークスティーリング

tokio は **ワークスティーリング（work-stealing）** アルゴリズムでタスクを分散する。各スレッドがローカルキューを持ち、自分のキューが空になったら**他のスレッドのキューからタスクを奪ってくる**。

```
ワークスティーリングの動作:

  Thread 1: [タスクA, タスクD, タスクF]  ← 忙しい
  Thread 2: []                          ← 暇
  Thread 3: [タスクE]

  → Thread 2 が Thread 1 からタスクF を奪う

  Thread 1: [タスクA, タスクD]
  Thread 2: [タスクF]            ← 仕事を取ってきた
  Thread 3: [タスクE]
```

Go の GMP スケジューラも同じ仕組みを採用している。**プログラマから見ると、どのスレッドで動いているかを意識する必要が一切ない**のがポイント。

### I/O 駆動のタスクスケジューリング（epoll / kqueue）

どのスレッドがリクエストを受け取るかは **OS のレベルで決まる**。tokio の各スレッドは OS の I/O 多重化機構（Linux: epoll、macOS: kqueue）を通じて「このソケットにデータが来た」という通知を受け取り、それをたまたま受け取ったスレッドが処理する。

```
リクエストの流れ:

1. Thread 1 がリクエストを受信（epoll/kqueue の通知）
2. Thread 1 が tokio::spawn でタスクを生成
   → 自分のローカルキューに入れる
3. Thread 2 が暇になる
   → 自分のキューが空なので Thread 1 のキューからタスクを奪う
4. タスクが I/O 待ちになる（DB の応答待ちなど）
   → そのタスクは一時停止し、スレッドは次のタスクを実行開始
```

### Node.js の Event Loop との対比

```
Node.js:
  ┌──────────────────────────┐
  │    1つの Event Loop       │  ← これが唯一の実行者
  │    全リクエストをここで処理 │
  └──────────────────────────┘

tokio（Rust）:
  ┌──────────┐ ┌──────────┐ ┌──────────┐
  │Event Loop│ │Event Loop│ │Event Loop│  ← 各スレッドが独自の
  │+ 実行機能│ │+ 実行機能│ │+ 実行機能│     Event Loop を持つ
  └──────────┘ └──────────┘ └──────────┘
```

tokio は **「Event Loop がスレッド数ぶん並列に動いている」** というイメージが最も近い。Node.js の Event Loop が 1 個しかないのに対し、tokio は CPU コア数ぶん動いている。Go も同じ考え方で、各 OS スレッド（P）がそれぞれローカルキューを持ち、互いにワークスティーリングし合う。

---

## 3. Rust による大規模 Web アプリケーションの構成パターン

Rust で大規模なバックエンド API を構築する際の一般的な構成パターンを示す。

### axum + tokio によるリクエスト処理

```rust
// main.rs — エントリポイント
#[tokio::main]
async fn main() -> anyhow::Result<()> {
    let config = Config::load()?;
    let state = AppState::new(&config).await?;

    let router = axum::Router::new()
        .route("/api/graphql", post(graphql_handler))
        .with_state(state);

    axum::Server::bind(&addr)
        .serve(router.into_make_service())
        .await?;
    Ok(())
}
```

`#[tokio::main]` マクロにより、マルチスレッドの tokio ランタイムが起動される。以降の全 async タスクはランタイムが管理する複数スレッドに自動で分散される。

### deadpool によるコネクションプーリング（primary / replica 分離）

```rust
#[derive(Clone)]
pub struct Database {
    primary: deadpool::managed::Pool<ConnectionManager>,
    readonly: deadpool::managed::Pool<ConnectionManager>,
}

impl Database {
    pub fn new(config: Config, primary_config: DbConfig, replica_config: DbConfig) -> Self {
        let primary = Pool::builder(ConnectionManager::new(primary_config))
            .max_size(config.max_pool_size_primary)
            .build()
            .unwrap();
        let replica = Pool::builder(ConnectionManager::new(replica_config))
            .max_size(config.max_pool_size_replica)
            .build()
            .unwrap();
        Self { primary, readonly: replica }
    }
}

// 参照クエリは自動的に replica に向かう
impl Queryable for Database {
    async fn query(&self, sql: &str, params: &[&dyn ToSql]) -> Result<Vec<Row>> {
        self.readonly.get().await?.query(sql, params).await
    }
}
```

- **deadpool** はコネクションプールの管理ライブラリで、tokio ランタイムと統合されている
- primary（書き込み用）と replica（読み取り用）を分離し、参照クエリを自動で replica に向ける構成が一般的
- プール内のコネクションは `recycle` で健全性をチェックし、異常なコネクションを自動破棄する

### Arc + Mutex による共有状態

Rust では `Arc`（Atomic Reference Counting）と `Mutex` を使って、複数タスク間でデータ構造を安全に共有する。

```rust
#[derive(Clone)]
pub struct AppState {
    config: &'static Config,
    database: Database,
    redis: RedisPool,
    cache: Arc<dyn Cache>,   // 全タスクから共有されるキャッシュ
}
```

起動時にマスタデータをメモリにロードし、全リクエストのタスクが同じキャッシュを直接参照できる：

```rust
// 起動時に並行してマスタデータをロード
let _ = futures_util::try_join!(
    state.database.load_holidays(),
    state.database.load_areas(),
    state.database.load_genres(),
)?;
```

全リクエストのタスクが**同じメモリ上のキャッシュ**を直接参照できるので、Redis へのラウンドトリップすら不要になる。

### mimalloc によるメモリアロケータ最適化

```rust
#[global_allocator]
static GLOBAL: mimalloc::MiMalloc = mimalloc::MiMalloc;
```

デフォルトのシステムアロケータの代わりに **mimalloc**（Microsoft が開発した高性能アロケータ）を使用するパターン。マルチスレッド環境でのメモリ割り当て性能が向上し、特に小さなオブジェクトの頻繁な確保・解放が多い Web アプリケーションで効果がある。

---

## 4. Node.js のマルチスレッド化手段とその限界

### Worker Threads の仕組みと制約

Node.js 10.5 から導入された Worker Threads は、1 プロセス内で複数スレッドを起動できる仕組み。ただし各スレッドが**独立した V8 エンジン（ヒープ）を持つ**のが Go/Rust との根本的な違い。

```
┌─────────────── 1つの Node.js プロセス ───────────────┐
│                                                      │
│  メインスレッド     Worker Thread 1   Worker Thread 2  │
│  [V8 インスタンス]  [V8 インスタンス]  [V8 インスタンス]  │
│  [独自のヒープ]     [独自のヒープ]     [独自のヒープ]     │
│                                                      │
│  ← SharedArrayBuffer でのみメモリ共有可能 →            │
└──────────────────────────────────────────────────────┘
```

共有できるのは `SharedArrayBuffer`（生のバイト列）だけで、普通の JavaScript オブジェクトは共有できない。

### Cluster モジュール

```
┌──────────────────────────────────────────────┐
│  マスタープロセス                               │
│  （リクエストを子プロセスに振り分ける）           │
│       ↓           ↓           ↓              │
│  [子プロセス1]  [子プロセス2]  [子プロセス3]     │
│  独立したメモリ  独立したメモリ  独立したメモリ    │
│  ポート共有      ポート共有      ポート共有       │
└──────────────────────────────────────────────┘
```

`fork()` で子プロセスを生成し、同じポートでリッスンする。本質的には ECS で複数コンテナを立てるのと同じ。

### 「同じ部屋で作業 vs 別々の部屋にメモ」の比喩

Go/Rust は **同じ部屋で複数人が同じホワイトボードを見ながら作業する** のに対し、Node.js の Worker Threads は **別々の部屋にいる人にメモを渡して作業してもらう** 感覚。

```
Go / Rust（1プロセス）:
┌──────────────────────────────────────┐
│  全タスクが同じメモリ空間を共有        │
│                                      │
│  タスクA ──→ Arc<HashMap> ←── タスクB │
│                  ↑                   │
│  タスクC ────────┘                   │
│                                      │
│  → 普通のデータ構造をそのまま共有可能   │
└──────────────────────────────────────┘

Node.js Worker Threads（1プロセス）:
┌──────────────────────────────────────┐
│  各スレッドが独立した V8 ヒープ        │
│                                      │
│  Thread A [ヒープA]  Thread B [ヒープB] │
│        ↘                ↙            │
│      SharedArrayBuffer               │
│      （生のバイト列のみ共有可能）       │
│                                      │
│  → オブジェクトの共有は不可能          │
│  → データ受け渡しはシリアライズが必要   │
└──────────────────────────────────────┘
```

| | Go / Rust | Node.js |
|---|---|---|
| メモリ共有 | 同一アドレス空間を自然に共有 | V8 ヒープは共有不可 |
| データの受け渡し | ポインタ/参照を渡すだけ（ゼロコスト） | シリアライズ → デシリアライズが必要 |
| 並列の粒度 | 関数呼び出し単位で気軽に並列化 | Worker 起動コストが高く、大きな単位でしか並列化しにくい |
| タスクの振り分け | **ランタイムが自動** | **プログラマが明示的に** |

Node.js の通常の Web サーバー（Express, Fastify 等）では、全リクエストがメインスレッドの Event Loop で処理される。Worker Threads を使うのは「画像リサイズ」「暗号化」「大量データの集計」など、明らかに CPU を食う処理を意図的に逃がす場合のみ。

---

## 5. DataLoader パターンの言語間比較

### DataLoader とは

GraphQL で N+1 問題を解決するパターン。短い時間窓の間に来た複数のデータ取得リクエストを1つにまとめてバッチ処理する。

```
GraphQL クエリ:
{
  items {              ← 20件返す
    name
    category { name }  ← 各アイテムのカテゴリを取得（20回呼ばれる）
  }
}

DataLoader なし: SELECT * FROM category WHERE id = ? を 20回
DataLoader あり: SELECT * FROM category WHERE id IN (1,2,...,20) を 1回
```

### Node.js: Event Loop の tick を利用（Mutex 不要、シンプル）

DataLoader は元々 Facebook が Node.js (JavaScript) 向けに作ったライブラリ。**シングルスレッドだからこそ自然に動く仕組み**。

```
Event Loop の 1 tick の中で:

  リゾルバA: loader.load(id=1)  → キューに追加
  リゾルバB: loader.load(id=2)  → キューに追加
  リゾルバC: loader.load(id=3)  → キューに追加
       ↓
  全リゾルバが同期的に実行し終わる
       ↓
  Event Loop の次の tick（process.nextTick / microtask）
       ↓
  キューに溜まった [1, 2, 3] をまとめて 1回の SQL で取得
```

```javascript
// Node.js 版 DataLoader の核心部分（簡略化）
load(key) {
  // Mutex 不要！シングルスレッドなので競合しない
  this._queue.push(key);

  if (!this._scheduled) {
    this._scheduled = true;
    process.nextTick(() => this._dispatch());
  }

  return this._promise(key);
}
```

### Rust: Mutex + oneshot channel（マルチスレッド対応）

Rust ではマルチスレッド環境で動作するため、共有状態へのアクセスに `Mutex` が必要。

```rust
// Rust 版 DataLoader の核心部分（簡略化）
async fn load(&self, key: K) -> V {
    let (tx, rx) = oneshot::channel();
    {
        let mut requests = self.requests.lock().unwrap();
        requests.keys.insert(key.clone());
        requests.pending.push((key, tx));
    }
    // バッチ実行後に oneshot channel 経由で結果を受け取る
    rx.await.unwrap()
}
```

### 効率は同等、差が出るのは DataLoader の「外側」

| | Node.js | Rust |
|---|---|---|
| DataLoader のバッチ化 | 効率的（Mutex 不要でむしろシンプル） | 効率的（Mutex が必要だが問題ない） |
| I/O 待ち | 効率的（Event Loop で並行処理） | 効率的（async/await で並行処理） |
| CPU 処理（JSON 化等） | **1 スレッドで直列** | **複数スレッドで並列** |
| 同時接続数が増えたとき | CPU 処理の直列がボトルネックに | スレッド数ぶんスケール |

DataLoader 単体で見ると効率は変わらない。差が出るのは **CPU を使う処理が積み重なったとき**。

```
1つの GraphQL クエリの処理全体:

  ① リクエスト受信・パース        ← CPU 処理
  ② リゾルバの実行               ← I/O 待ち（DB, Redis）
  ③ DataLoader のバッチ SQL 実行  ← I/O 待ち
  ④ レスポンスの組み立て・JSON 化  ← CPU 処理

Node.js の問題:
  ①④ の CPU 処理中、他のリクエストの ①④ は待たされる
  （Event Loop が 1 つなので）

Rust/Go:
  ①④ の CPU 処理も複数スレッドで並列実行される
```

---

## 6. バックエンド言語選択の判断基準

### 性能だけではなく、採用・エコシステム・チーム構成

バックエンド言語の選択は性能だけで決まるものではない。以下の観点を総合的に判断する必要がある。

### Node.js (TypeScript) が選ばれる現実的な理由

**1. 採用・チーム構成**

これが最大の理由。スタートアップでエンジニア 3〜5 人の場合、全員がフロントもバックもやるため、言語を統一した方が全員が全コードを読める。Rust や Go を書ける人材は TypeScript を書ける人材より少ない。

**2. エコシステムの共有**

フロントとバックで共有できるものが多い：
- バリデーションロジック（zod, yup 等）
- 型定義（GraphQL codegen, tRPC 等）
- ユーティリティ（日付処理、文字列処理等）
- テストツール（Jest, Vitest 等）

tRPC のように**フロントとバックで型を完全に共有する**仕組みは、同じ言語でないと実現できない。

**3. 「十分速い」ケースが多い**

```
典型的な Web API のレイテンシ内訳:

  DB クエリ:        50ms  ← ボトルネックはほぼここ
  ネットワーク:      20ms
  外部 API 呼び出し: 100ms
  アプリの処理:       5ms  ← Go なら 1ms, Rust なら 0.5ms

  合計: 175ms vs 171ms → ユーザーには区別がつかない
```

I/O が支配的な API では、言語の処理速度は全体のごく一部。

### Rust/Go が有利な条件

以下の条件が揃う場合、Rust/Go の採用が合理的：

- 高トラフィック
- インメモリキャッシュの共有が重要（マスタデータ等）
- DataLoader によるバッチ集約が多用される
- レイテンシ要件が厳しい（ユーザー向けサービス）
- GC pause が許容しにくい（安定した応答時間が求められる）※ Rust の場合
- Rust/Go を書けるチームがいる

### Node.js が「十分」な条件

- I/O 中心の CRUD API
- トラフィックが中程度
- チームの大半が TypeScript に慣れている
- フロントエンドとの型共有が重要

### 判断フロー

```
言語選択の判断フロー（バックエンド）:

  チームが Rust/Go を書ける？
    ├─ No → TypeScript で十分なケースが多い
    └─ Yes → 要件次第
                ├─ I/O 中心の CRUD API → どれでも大差ない
                ├─ 高トラフィック + 共有状態 → Rust / Go が有利
                └─ 極限のレイテンシ要件 → Rust が最適
```

「Node.js にメリットがない」というよりは、**「性能が必要な場面では Go/Rust の方が自然に書ける」が、「多くの Web アプリは性能がボトルネックではない」** というのが実態。

---

## 付録: 用語集

| 用語 | 説明 |
|---|---|
| **tokio** | Rust の非同期ランタイム。マルチスレッドでの async/await を実現する |
| **axum** | tokio 上で動作する Web フレームワーク |
| **deadpool** | Rust のコネクションプーリングライブラリ |
| **mimalloc** | Microsoft が開発した高性能メモリアロケータ |
| **Arc** | Atomic Reference Counting。スレッド間で安全にデータを共有するスマートポインタ |
| **Mutex** | Mutual Exclusion。共有データへの排他アクセスを保証する |
| **ワークスティーリング** | 暇なスレッドが忙しいスレッドのキューからタスクを奪う負荷分散アルゴリズム |
| **epoll / kqueue** | Linux / macOS の I/O 多重化機構 |
| **Event Loop** | Node.js の実行モデル。シングルスレッドで I/O を非同期に処理する |
| **Worker Threads** | Node.js で複数スレッドを起動する仕組み（V8 ヒープは分離） |
| **DataLoader** | GraphQL の N+1 問題を解決するバッチ化パターン |
| **GMP スケジューラ** | Go のランタイムスケジューラ（Goroutine, Machine, Processor） |
