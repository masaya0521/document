# Tech Updates — 2026-06-26

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Angular | v22 リリース（6/3） | Selectorless Components、Signal Forms 安定化、Angular ARIA / MCP server 安定化。OnPush・Incremental Hydration がデフォルトに | [公式ブログ](https://blog.angular.dev/) / [ANGULARarchitects](https://www.angulararchitects.io/en/blog/angular-22-the-most-important-new-features-at-a-glance/) |
| 2 | PostgreSQL | 19 Beta 1 リリース（6/4） | SQL/PGQ プロパティグラフ、`ON CONFLICT DO SELECT`、`REPACK`、並列 autovacuum、MultiXactOffset の 64bit 化。GA は 9〜10 月予定 | [公式ニュース](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/) |
| 3 | Node.js | セキュリティリリース（6/18） | 22.23.0 / 24.17.0 / 26.3.1 を同時公開。12 件の CVE 修正（うち HIGH 2 件：WebCrypto クラッシュ、TLS ワイルドカード bypass） | [公式ブログ](https://nodejs.org/en/blog/vulnerability/june-2026-security-releases) |
| 4 | FastAPI | `app.frontend()` 追加（〜6/20） | `dist` ディレクトリから SPA を配信する `app.frontend()` / `router.frontend()` を追加。ルーター内部のリファクタで `.matches()` / `.handle()` を追加 | [Release Notes](https://fastapi.tiangolo.com/release-notes/) |
| 5 | Visual Studio Code | 1.126 リリース（6/24） | セッション単位のコスト表示、1 セッション内で複数チャット並走、未知フォルダの restricted mode（Workspace Trust） | [公式 Updates](https://code.visualstudio.com/updates/v1_126) |
| 6 | Svelte / SvelteKit | 月次更新（svelte@5.56.0 / SvelteKit 2.61.0） | SvelteKit で `query.live(...)` の長期接続サポート、`.run()` を削除（`await query()` へ）。`query.batch(...)` 追加。TypeScript 6.0 対応 | [公式ブログ](https://svelte.dev/blog/whats-new-in-svelte-june-2026) |
| 7 | Redis Insight | 3.4.1 GA リリース | 専用 Search ワークスペース（インデックスのライフサイクル管理）、Redis 8.8 対応、Linux ARM64 パッケージ（AppImage/deb/rpm）追加 | [endoflife.date](https://endoflife.date/redis) / [releases.sh](https://releases.sh/redis/releases) |
| 8 | Next.js | 16.2.x セキュリティ修正（6 月） | RSC レスポンスのキャッシュポイズニング等、Server Components / App Router / Middleware / Proxy にまたがる複数の脆弱性を修正 | [Next.js Updates](https://releasebot.io/updates/vercel/next-js) |
| 9 | Tailwind CSS | `@tailwindcss/vite` 4.3.1（〜6 月中旬） | Tailwind v4 系の Vite プラグインを継続更新。PostCSS 経由より高速なビルドを提供 | [npm](https://www.npmjs.com/package/@tailwindcss/vite) |
| 10 | Bun | 1.3.11（6 月） | 統合 dev サーバー・パッケージセキュリティスキャナ等を備える 1.3 系の最新パッチ。ES decorators / Windows ARM64 対応 | [GitHub Releases](https://github.com/oven-sh/bun/releases) |

## Deep Dive

- [Angular 22 — Signal-First 時代の本格到来](./tu-angular-22.md)
- [PostgreSQL 19 Beta 1 — グラフクエリ・REPACK・並列 autovacuum](./tu-postgresql-19-beta.md)
