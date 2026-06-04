# Tech Updates — 2026-06-05

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Angular | v22.0 リリース（6/3） | Signal Forms / Resource API / Angular Aria が安定化。OnPush・Fetch・strictTemplates がデフォルト化、TypeScript 6 必須、Node 20 サポート終了。`@Service()` デコレータや WebMCP 連携を追加 | [Ninja Squad](https://blog.ninja-squad.com/2026/06/03/what-is-new-angular-22.0), [angular.dev](https://angular.dev/events/v22) |
| 2 | Go | 1.26.4 / 1.25.11（6/2） | セキュリティ修正リリース。crypto/x509・mime・net/textproto の脆弱性修正に加え、コンパイラ・ランタイム・go fix・crypto/fips140 のバグ修正 | [Go release history](https://go.dev/doc/devel/release), [golang-announce](https://groups.google.com/g/golang-announce/c/uVOCkuwbiD8) |
| 3 | Python | 3.15.0b2（6/2） | 3.15 の第2ベータ。フィーチャーフリーズ後の安定化フェーズで、新機能の検証・バグ修正が中心 | [python.org downloads](https://www.python.org/downloads/source/), [Status of Python versions](https://devguide.python.org/versions/) |
| 4 | pnpm | 11.3 リリース | npm のステージド公開（staged publishing）対応、`trustLockfile` 設定、`pnpm pkg`/`pnpm repo`/`pnpm set-script` のネイティブ実装を追加。直前の 11.2 では Rust 移植版 pacquet を実験的に opt-in 可能に | [pnpm blog](https://pnpm.io/blog), [pnpm 11.2](https://pnpm.io/blog/releases/11.2) |
| 5 | PostgreSQL | 18.4 / 17.10 / 16.14 / 15.18 / 14.23（5/14） | セキュリティアップデート。11 件の脆弱性と 60 件超のバグを修正。tzdata 2026b へ更新（11月以降のブリティッシュコロンビア州の恒久DST 等を反映） | [PostgreSQL News](https://www.postgresql.org/about/news/postgresql-184-1710-1614-1518-and-1423-released-3297/) |
| 6 | Ruby | 4.0.4 リリース（5/11） | 4.0 安定版系列のメンテナンスリリース。バグ修正を中心とした定期更新 | [Ruby News](https://www.ruby-lang.org/en/news/2026/05/11/ruby-4-0-4-released/), [Ruby Releases](https://www.ruby-lang.org/en/downloads/releases/) |
| 7 | VS Code | 1.122（May 2026 系） | 5月は v1.119〜v1.122 を出荷。Agents ウィンドウの Stable プレビュー化、インライン補完の静粛化、Markdown プレビュー/ノートブック/チャットへの Mermaid 図ネイティブレンダリング内蔵などを追加 | [VS Code Updates](https://code.visualstudio.com/updates/), [microsoft/vscode releases](https://github.com/microsoft/vscode/releases) |
| 8 | Bun | 1.3 系（最新 1.3.11） | フルスタック開発機能を統合した大型リリース。ゼロコンフィグのフロントエンド開発（HMR/React Fast Refresh）、MySQL/MariaDB/PostgreSQL/SQLite を統一的に扱う `Bun.SQL`、メモリ使用量 10〜30% 削減等の性能改善 | [Bun blog](https://bun.sh/blog), [InfoQ](https://www.infoq.com/news/2026/01/bun-v3-1-release/) |
| 9 | Deno | 2.8 リリース | 2.0 で始まった Node.js 互換作業を完了。package.json・node_modules・npm workspaces・大半の CommonJS パッケージが摩擦なく動作。先行する 2.7 では Temporal API を安定化 | [Deno blog](https://deno.com/blog), [daily.dev](https://daily.dev/blog/javascript-runtimes-bun-vs-node-js-vs-deno-comparison/) |
| 10 | Tailwind CSS | 4.2.x（Vite 8 対応） | v4.2.0 で webpack プラグインと4つの新カラーパレット、logical property ユーティリティを追加。v4.2.2 で Vite 8 を正式サポート（peer dependency に `^8.0.0` を追加） | [Tailwind blog](https://tailwindcss.com/blog), [InfoQ](https://www.infoq.com/news/2026/04/tailwind-css-4-2-webpack/) |

## Deep Dive

- [Angular 22 — Signal-First 時代の確立とメジャー破壊的変更](./tu-angular-22.md)
- [Go 1.26 — Green Tea GC のデフォルト化と性能改善](./tu-go-1-26.md)
