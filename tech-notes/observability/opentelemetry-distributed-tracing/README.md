# OpenTelemetry と分散トレーシングの全体像

## この文書が答える問い

「分散トレーシングとは何か、OpenTelemetry はどのような構成で導入され、フロントエンドからバックエンドまでの end-to-end トレーシングはどう実現されるのか」

## 結論

- 分散トレーシングは **Trace ID** を使って複数サービスにまたがるリクエストを1つの処理として追跡する仕組み
- OpenTelemetry は計装（instrumentation）とエクスポートを分離し、ベンダーロックインなしに導入できる
- フロントエンドが `traceparent` ヘッダを送信し、バックエンドがそれを受信・紐づけするだけで end-to-end のトレースが成立する

---

## 1. 分散トレーシングの基本概念

### Trace と Span

- **Trace**: 1つのリクエストがシステムを通過する全体の記録。一意な Trace ID を持つ
- **Span**: Trace を構成する個々の処理区間。開始/終了時刻、属性（attributes）、親子関係を持つ

```
Trace (trace-id: abc123)
├── Span: HTTP GET /api/restaurants (50ms)
│   ├── Span: GraphQL execute (45ms)
│   │   ├── Span: DB Query - restaurants (10ms)
│   │   └── Span: DB Query - plans (8ms)
│   └── Span: Auth Session 取得 (5ms)
```

Span のツリー構造がリクエストの処理フローそのものを表現する。

### なぜ必要か

モノリスなら1プロセス内でログを追えるが、マイクロサービスやフロントエンド/バックエンド分離の構成では、1リクエストが複数のサービスに分散する。各サービスのログを個別に見ても全体像が掴めない。Trace ID で横断的に紐づけることで:

- どのサービスのどの処理がボトルネックか一目でわかる
- エラーの根本原因をサービスを跨いで追跡できる

---

## 2. W3C Trace Context（トレース伝播）

サービス間でトレース情報を受け渡す W3C 標準。HTTP ヘッダ `traceparent` を使う。

```
traceparent: 00-4bf92f3577b34da6a3ce929d0e0e4736-00f067aa0ba902b7-01
              │  │                                │                │
              ver │                                parent-span-id  sampling flag
                  trace-id (16 bytes)
```

| フィールド | 役割 |
|-----------|------|
| **trace-id** | リクエスト全体を識別する ID。全サービスで共通 |
| **parent-span-id** | 呼び出し元サービスのスパン ID |
| **sampling flag** | `01` = サンプリング対象、`00` = 対象外 |

### 伝播の流れ

```
Service A                          Service B
─────────                          ─────────
1. Span 作成 (span-id: 001)
2. HTTP リクエスト送信
   Header: traceparent: 00-{traceId}-001-01
                                    3. ヘッダから traceId, parentSpanId を抽出
                                    4. Span 作成 (span-id: 002, parent: 001)
                                    5. 同じ traceId でログ・スパンを記録
```

これにより、異なるサービスのスパンが同じ Trace に属し、親子関係も保持される。

---

## 3. OpenTelemetry の構成

### OpenTelemetry とは

計装（データ収集）とエクスポート（データ送信先）を分離する、ベンダー非依存のオブザーバビリティフレームワーク（CNCF プロジェクト）。

### 3つのシグナル

| シグナル | 何がわかるか | 例 |
|---------|------------|-----|
| **Traces** | リクエストの流れと所要時間 | API → DB の呼び出しチェーン |
| **Metrics** | システムの定量状態 | リクエスト数、レイテンシ分布 |
| **Logs** | 個別イベント記録 | エラーメッセージ |

### アーキテクチャ

```
アプリケーションコード
  ↓ (OpenTelemetry SDK で計装)
Exporter
  ↓ (設定で切り替え可能)
Google Cloud Trace / Datadog / Jaeger / Grafana Tempo / ...
```

計装を1回書けば、エクスポート先をコード変更なしで切り替えられるのが最大の利点。

---

## 4. バックエンドでの典型的なトレーシング構成

### 4.1 初期化

環境変数（例: `OTEL_SERVICE_NAME`）でモードを切り替えるのが一般的:

- **本番**: OpenTelemetry Exporter → クラウドのトレースサービスに送信
- **開発**: stdout にログ出力（Exporter なし）

### 4.2 自動計装（Instrumentation）

フレームワークのミドルウェア/インターセプターで、コードを書かずにスパンを生成する。

**HTTP レイヤー（ミドルウェア）**:
- リクエスト受信時にスパンを自動作成
- method, route, status_code, duration 等を記録
- `traceparent` ヘッダから親コンテキストを抽出して紐づけ

**GraphQL レイヤー（Extension / Plugin）**:
- request → parse → execute の各フェーズでスパン生成
- operation name やクエリ内容を属性に記録

**DB / ORM レイヤー**:
- クエリ実行をスパンとして記録

### 4.3 カスタム計装

自動計装でカバーできない処理は手動でスパンを作成する:

```
// 擬似コード
span = startSpan("external-api-call")
span.setAttribute("api.endpoint", url)
result = httpClient.get(url)
span.setAttribute("http.status_code", result.status)
span.end()
```

`span.record()` / `span.setAttribute()` で後から属性を追加するパターンが多い。

### 4.4 セキュリティ考慮

トレースやログに機密情報が混入しないよう、以下の対策を行う:

- メールアドレス・電話番号等の自動マスキング
- リクエストボディの記録を避ける、または選択的に記録

---

## 5. フロントエンドからの end-to-end トレーシング

### 現状（フロントエンド未計装の場合）

```
ブラウザ ──(traceparent なし)──→ バックエンド → DB
                                 ├─ ここからはトレースあり
```

バックエンド内のトレースは取れるが、「どの画面のどの操作がこのリクエストを発生させたか」は不明。

### フロントエンド計装後

```
ブラウザ ──(traceparent: 00-{traceId}-{spanId}-01)──→ バックエンド → DB
├─ ブラウザ側スパン                                     ├─ 同じ traceId で紐づく
```

### 実現できること

| 観点 | フロントエンド未計装 | フロントエンド計装済み |
|------|-------------------|---------------------|
| バックエンドのボトルネック特定 | 可能 | 可能 |
| 「どの画面操作が原因か」の特定 | 不可 | **可能** |
| ブラウザ → DB の end-to-end レイテンシ | 不可 | **可能** |
| フロントエンドエラーとバックエンドログの紐づけ | 不可 | **可能** |

### 実装アプローチ: ブラウザ計装 vs SSR/BFF サーバー計装

フロントエンドの計装には2つのアプローチがある。

#### アプローチ A: ブラウザ側で計装

```
ブラウザ (sdk-trace-web) ──traceparent──→ API サーバー → DB
```

`@opentelemetry/sdk-trace-web` をブラウザに導入し、fetch に `traceparent` を自動付与する。

**課題**:
- **Zone.js 依存**: 非同期コンテキスト伝播に Zone.js を使うのが標準だが、Zone.js は `Promise`・`setTimeout`・`fetch` 等をグローバルにモンキーパッチする。React の Concurrent Mode と干渉するリスクがあり、React/Next.js プロジェクトでは避けたい
- **バンドルサイズ**: OTel SDK + Zone.js で ~50KB (gzipped) 程度の追加
- **CORS**: ブラウザから Trace Backend に直接エクスポートする場合、CORS 設定が必要

ただし、fetch instrumentation だけなら Zone.js なしでも動作する。困るのはブラウザ内の非同期処理の親子関係を自動追跡したい場合。

#### アプローチ B: SSR/BFF サーバー（Node.js）で計装（推奨）

```
ブラウザ → Next.js (Node.js / sdk-node) ──traceparent──→ API サーバー → DB
           ここで計装
```

Next.js 等の SSR/BFF 構成では、**API サーバーへの fetch は Node.js プロセスから発行される**。そのため:

- `@opentelemetry/sdk-node` (Node.js 向け SDK) を使える。バックエンドと同じ安定した仕組み
- Zone.js 不要、バンドルサイズ影響なし（サーバーサイド）
- fetch / http モジュールの自動計装がそのまま使える
- CORS の問題もなし

**トレースしたい情報のほとんどは API 呼び出し（fetch）に関するもの**なので、SSR/BFF 構成であれば Node.js 側の計装だけで end-to-end トレーシングの主要な価値は得られる。

#### ブラウザ計装が必要になるケース

- クライアントサイドから直接 API を叩く構成（CSR のみの SPA）
- ブラウザでの描画時間や Core Web Vitals まで計測したい場合
- ユーザー操作（クリック → 画面遷移）単位でトレースを切りたい場合

### 判断基準

| | ブラウザ計装 | SSR/BFF サーバー計装 |
|---|---|---|
| API → DB のトレース | 可能 | 可能 |
| Zone.js リスク | あり | なし |
| バンドルサイズ影響 | ~50KB gzipped | なし |
| 導入の容易さ | やや手間 | シンプル |
| ブラウザ描画の計測 | 可能 | 不可 |
| 推奨される構成 | CSR SPA | SSR / BFF |

---

## 6. 典型的な構成図

### SSR/BFF 構成（推奨）

```
┌──────────────────────────────┐
│ ブラウザ                       │
│  (計装なし)                    │
└──────────────┬───────────────┘
               │ HTTP
               ↓
┌──────────────────────────────────────────────────────────┐
│ SSR / BFF サーバー (Next.js 等)                            │
│  @opentelemetry/sdk-node                                  │
│  ├─ fetch/http instrumentation (traceparent 自動付与)      │
│  └─ Exporter → Trace Backend                              │
└──────────────┬───────────────────────────────────────────┘
               │ HTTP + traceparent header
               ↓
┌──────────────────────────────────────────────────────────┐
│ API サーバー                                               │
│  OpenTelemetry SDK                                        │
│  ├─ HTTP ミドルウェア (自動スパン + traceparent 抽出)        │
│  ├─ GraphQL Extension (request/parse/execute スパン)       │
│  ├─ カスタムスパン (外部 API 呼び出し等)                     │
│  ├─ セキュリティ (機密情報マスキング)                        │
│  └─ Exporter → Trace Backend                              │
└──────────────┬───────────────────────────────────────────┘
               │
               ↓
┌──────────────────────────────────────────────────────────┐
│ Trace Backend                                             │
│  (Google Cloud Trace / Datadog / Jaeger / Grafana Tempo)  │
│  ├─ トレースのツリー表示                                    │
│  ├─ レイテンシ分析                                         │
│  └─ ログとの相関                                           │
└──────────────────────────────────────────────────────────┘
```

### ブラウザ計装構成（CSR SPA 向け）

```
┌──────────────────────────────────────────────────────────┐
│ ブラウザ                                                   │
│  @opentelemetry/sdk-trace-web                             │
│  ├─ fetch instrumentation (traceparent 自動付与)           │
│  └─ OTLP Exporter → Trace Backend                        │
└──────────────┬───────────────────────────────────────────┘
               │ HTTP + traceparent header
               ↓
┌──────────────────────────────────────────────────────────┐
│ API サーバー (同上)                                        │
└──────────────────────────────────────────────────────────┘
```

---

## 7. 深掘りテーマ

### サンプリング戦略

全トレースを記録する AlwaysOn サンプリングはデバッグに最適だが、トラフィック増加時にはコストとパフォーマンスの問題が出る。Head-based（リクエスト開始時に判定）vs Tail-based（リクエスト完了後に判定）の違い、エラー発生時だけ記録する戦略など、本番運用におけるサンプリング設計。

### OpenTelemetry Collector

アプリから直接エクスポートする構成と、間に Collector を挟む構成のトレードオフ。Collector を使うとフィルタリング・バッチ処理・複数エクスポート先への分岐が柔軟になる。サイドカー vs ゲートウェイ構成の選択基準。

### トレースとログの相関（Correlation）

Trace ID をログに埋め込んで、トレースビューからログにジャンプできるようにする仕組み。構造化ログに `trace_id` / `span_id` フィールドを含めることで、ログ検索とトレース表示を行き来できる。

### コンテキスト伝播の落とし穴

非同期処理やメッセージキューを挟む場合にコンテキストが途切れる問題。キューに Trace Context をメタデータとして載せる方法、バッチ処理での新規トレース vs 継続トレースの判断基準など。
