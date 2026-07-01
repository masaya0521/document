# Tech Updates — 2026-07-02

開発者が日常的に使う技術（フレームワーク・言語・ランタイム・ツール）の直近のリリース・アップデート情報を10件厳選。

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | v7.0 RC（2026-06-18） | コンパイラを Go でネイティブ移植（tsgo）。型チェックが 6.0 比で約10倍高速。RC は npm 公開済みで、安定版は約1ヶ月以内を予定 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-rc/) |
| 2 | Angular | v22.0（2026-06-03） | Signal Forms・Resource API・Angular Aria が安定化。変更検出のデフォルトが OnPush に、HttpClient が Fetch API デフォルトに。TypeScript 6 必須 | [Ninja Squad](https://blog.ninja-squad.com/2026/06/03/what-is-new-angular-22.0), [angular.dev](https://angular.dev/events/v22) |
| 3 | Node.js | v24.18.0（LTS, 2026-06-23） | Active LTS「24」系の最新パッチ。V8 13.6 ベース（Explicit Resource Management の `using`、`Float16Array`、`RegExp.escape()` 等） | [Node.js Releases](https://nodejs.org/en/about/previous-releases) |
| 4 | VS Code | v1.126（2026-06-24） | セッション単位のコスト表示、1つの Agent セッションで複数チャット並列、新規フォルダのデフォルト Restricted Mode 化、モデル調整 UI の統合 | [Release Notes](https://code.visualstudio.com/updates/v1_126) |
| 5 | Rust | v1.96.0（2026-05-28） | RFC 3550 によりレンジ型のエルゴノミクス問題を解消。新アサーションマクロ2種を安定化。サードパーティレジストリ向けの CVE 2件を同梱修正 | [Rust Blog](https://blog.rust-lang.org/2026/05/28/Rust-1.96.0/) |
| 6 | Python | v3.14.6（2026-06-10） | 3.14 系6回目のメンテナンスリリース（約179件のバグ修正）。3.14 は free-threaded（PEP 779）が正式サポート化された系列 | [python.org](https://www.python.org/downloads/release/python-3146/) |
| 7 | Bun | v1.3.x（2026, 継続リリース） | 1.3 でゼロコンフィグのフロントエンド開発・統一 SQL API（`Bun.SQL`）・組み込み Redis クライアント・VS Code Test 連携を導入。以降パッチで安定化 | [Bun Blog](https://bun.com/blog/bun-v1.3) |
| 8 | Kubernetes | v1.34.9（2026-06-09） | 1.34 系の最新パッチ。1.34 は DRA（Dynamic Resource Allocation）安定化、Linux ノードの swap 対応など58の機能強化を含む | [Kubernetes 1.34](https://kubernetes.io/releases/1.34/), [Patch Releases](https://kubernetes.io/releases/patch-releases/) |
| 9 | Vite | v8.0（2026-03-12） | バンドラを Rust 製 Rolldown に一本化（従来は esbuild + Rollup）。ビルドが最大10〜30倍高速化。Linear で 46s→6s の実績 | [Vite Blog](https://vite.dev/blog/announcing-vite8) |
| 10 | PostgreSQL | v18.4（2026-05-14） | PostgreSQL 18 系の最新マイナー。18 は新 I/O サブシステムで読み込み最大3倍、B-tree の skip scan、`uuidv7()`、OAuth 2.0 認証等を導入 | [Release Notes](https://www.postgresql.org/docs/release/18.4/), [PG18](https://www.postgresql.org/about/news/postgresql-18-released-3142/) |

## Deep Dive

- [TypeScript 7.0 RC — Go ネイティブコンパイラ](./tu-typescript-7-0-rc.md)
- [Angular 22 — Signal Forms / OnPush デフォルト化 / Fetch 標準化](./tu-angular-22.md)
