# Tech Updates — 2026-06-11

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Apple Xcode / Foundation Models | WWDC 2026 で Xcode 27・各種フレームワーク発表（6/8） | Xcode 27 が Anthropic・Google・OpenAI のエージェント統合、MCP 対応、Apple silicon 専用化でサイズ 30% 削減。Foundation Models は画像入力対応とサーバー側モデル呼び出しを追加 | [Apple Newsroom](https://www.apple.com/newsroom/2026/06/apple-aids-app-development-with-new-intelligence-frameworks-and-advanced-tools/) |
| 2 | VS Code | v1.124 リリース（6/10） | Autopilot がデフォルト有効化されタスク完了判定を高度化。バックグラウンドセッション、セッションナビゲーション、統合ブラウザの履歴検索を追加 | [Release Notes](https://code.visualstudio.com/updates/v1_124) |
| 3 | Svelte / SvelteKit | 2026年6月アップデート（v2.61.0） | リモートクエリを各コンテキストで await 可能に、キャッシュ重複排除に対応。`query.live(...)` が本格利用可能に。TypeScript 6.0 対応。enhance コールバックの引数仕様変更など破壊的変更あり | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-june-2026) |
| 4 | PostgreSQL | 19 Beta 1 リリース（6/4） | 非同期 I/O（AIO）の自動ワーカースケーリング、パラレル autovacuum、INSERT 高速化。`EXPLAIN ANALYZE` に IO オプション追加。GA は 2026年9-10月頃を予定 | [PostgreSQL News](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/) |
| 5 | Python | 3.15 フィーチャーフリーズ / 3.14.6 パッチ（6/10） | Python 3.15 がフィーチャーフリーズに到達。同日に安定版 3.14 系のメンテナンスリリース 3.14.6 も公開 | [Real Python](https://realpython.com/python-news-june-2026/) |
| 6 | Chrome / DevTools | Chrome 139 安定版 | Web Speech API のオンデバイス音声認識、CSS Corner Shaping（squircle 等）、CSS Custom Functions を追加。DevTools は既知の不具合を整理し未解決 issue を 27% 削減 | [New in Chrome 139](https://developer.chrome.com/blog/new-in-chrome-139) |
| 7 | Redis / node-redis | Redis 8.8 / node-redis 6.0 | Redis 8.8 でクライアントライブラリ対応強化、Redis Insight 3.4.1 GA。node-redis 6.0 は初のメジャー更新で RESP3 をデフォルト化 | [releases.sh](https://releases.sh/redis/releases) |
| 8 | GitHub CLI | sub-issue・依存関係の管理対応（6/10） | `gh` でサブ課題・親子関係・依存関係をターミナルから直接操作可能に。Discussions 操作の `gh discussion` コマンド群も追加 | [GitHub Changelog](https://github.blog/changelog/month/06-2026/) |
| 9 | GitHub Copilot CLI | `/security-review` コマンド公開プレビュー（6/10） | コード変更に対する AI 駆動のセキュリティレビューをターミナルから実行できる試験的スラッシュコマンドを追加 | [GitHub Changelog](https://github.blog/changelog/2026-06-10-dedicated-security-review-command-now-available-in-copilot-cli/) |
| 10 | Dependabot | Deno エコシステム対応（6/9） | Dependabot のバージョン更新機能が Deno エコシステムをサポート開始。CodeQL 2.25.6（6/5）も Swift 6.3.2 対応で同週リリース | [GitHub Changelog](https://github.blog/changelog/month/06-2026/) |

## Deep Dive

- [Apple WWDC 2026 — Xcode 27 と Intelligence フレームワーク](./tu-apple-wwdc-2026-xcode-27.md)
- [PostgreSQL 19 Beta 1 — 非同期 I/O とパラレル autovacuum](./tu-postgresql-19-beta-1.md)
