# Tech Updates — 2026-06-19

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Node.js | v22.23.0 / v24.17.0 / v26.3.1 セキュリティリリース | 全サポートラインに影響する 12 件の CVE を修正。WebCrypto の整数オーバーフロー（DoS）と TLS ワイルドカード認証バイパスが HIGH。早急なアップデートを推奨 | [Node.js Blog](https://nodejs.org/en/blog/vulnerability/june-2026-security-releases) |
| 2 | Visual Studio Code | v1.125 リリース | 統合ブラウザの強化（Web 検索・リモート接続越しの閲覧）、拡張機能アップデートの待機時間制御、Copilot のエンタープライズ管理強化 | [VS Code Updates](https://code.visualstudio.com/updates/v1_125) |
| 3 | Tailwind CSS | v4.3.1 リリース | 4.x 系の最新パッチ。現在アクティブサポートは 2 バージョン体制（4.3 系と 3.4 系） | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases) |
| 4 | Angular | v22.0.0 リリース | Signal Forms・resource()・httpResource が stable 化。OnPush がデフォルトの変更検知戦略に。WebMCP で AI エージェント連携。"signal-first" 時代へ | [Angular.love](https://angular.love/angular-22-key-features-and-changes) |
| 5 | PostgreSQL | 19 Beta 1 リリース | 次期メジャーバージョン 19 のベータ第1弾。本番投入前の検証フェーズ開始 | [PostgreSQL News](https://www.postgresql.org/docs/release/) |
| 6 | Go | v1.26.4 リリース | 1.26 系のパッチリリース。バグ修正・セキュリティ対応 | [Go Release History](https://go.dev/doc/devel/release) |
| 7 | CloudNativePG | v1.29.1 / v1.28.3 リリース | PostgreSQL Operator の重要セキュリティ修正（CVE-2026-44477）と HA 関連の修正。Kubernetes 上で Postgres を運用する環境は要更新 | [CloudNativePG Releases](https://cloudnative-pg.io/releases/) |
| 8 | Bun | v1.3.x（最新 1.3.11） | TC39 標準 ES Decorators 対応、Windows ARM64 サポート。1.3 系では MySQL / Redis 組み込みクライアントや zero-config フロントエンド開発を提供 | [LogRocket Blog](https://blog.logrocket.com/bun-javascript-runtime-taking-node-js-deno/) |
| 9 | Supabase (Multigres) | v0.1 alpha 公開 | Postgres をスケーラブルに運用する OSS。シャーディング・コネクションプーリング・自動フェイルオーバー・バックアップ統制を提供する "Postgres 向け OS" | [Supabase Changelog](https://supabase.com/changelog/46689-developer-update-june-2026) |
| 10 | WordPress (Gutenberg) | v23.3 / v23.2 リリース | エディタ更新の大型ロット。5 つの新ウィジェット、Site Health / News / Events、サイトプレビュー URL バー、コンテナブレークポイント対応グリッド列など | [WordPress Developer Blog](https://developer.wordpress.org/news/2026/06/whats-new-for-developers-june-2026/) |

## Deep Dive

- [Angular 22 — signal-first 時代の到来](./tu-angular-22.md)
- [Node.js 2026年6月セキュリティリリース — 全ラインに影響する 12 CVE](./tu-nodejs-june-2026-security.md)
