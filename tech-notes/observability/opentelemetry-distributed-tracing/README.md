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

### フロントエンド側の実装アプローチ

JavaScript/TypeScript 向けには `@opentelemetry/sdk-trace-web` が標準ライブラリ:

1. **TracerProvider の初期化**: エクスポート先の設定
2. **fetch / XMLHttpRequest の自動計装**: `@opentelemetry/instrumentation-fetch` が `traceparent` ヘッダを自動付与
3. **エクスポート**: OTLP Exporter でバックエンドと同じトレースサービスに送信

バックエンド側が既に `traceparent` の受信・親スパン紐づけを実装済みであれば、**フロントエンドがヘッダを送るだけで end-to-end のトレースが成立する**。

---

## 6. 典型的な構成図

```
┌─────────────────────────────────────────────────────────┐
│ ブラウザ                                                  │
│  @opentelemetry/sdk-trace-web                            │
│  ├─ fetch instrumentation (traceparent 自動付与)          │
│  └─ OTLP Exporter → Trace Backend                       │
└────────────────┬────────────────────────────────────────┘
                 │ HTTP + traceparent header
                 ↓
┌─────────────────────────────────────────────────────────┐
│ API サーバー                                              │
│  OpenTelemetry SDK                                       │
│  ├─ HTTP ミドルウェア (自動スパン + traceparent 抽出)       │
│  ├─ GraphQL Extension (request/parse/execute スパン)      │
│  ├─ カスタムスパン (外部 API 呼び出し等)                    │
│  ├─ セキュリティ (機密情報マスキング)                       │
│  └─ Exporter → Trace Backend                             │
└────────────────┬────────────────────────────────────────┘
                 │
                 ↓
┌─────────────────────────────────────────────────────────┐
│ Trace Backend                                            │
│  (Google Cloud Trace / Datadog / Jaeger / Grafana Tempo) │
│  ├─ トレースのツリー表示                                   │
│  ├─ レイテンシ分析                                        │
│  └─ ログとの相関                                          │
└─────────────────────────────────────────────────────────┘
```
