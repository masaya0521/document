# Tech Updates — 2026-05-27

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Kotlin | KotlinConf 2026 / VS Code Alpha | KotlinConf 2026 にて Kotlin 2.4 プレビュー、Kotlin for VS Code Alpha、Exposed 1.0 安定版、Koog 1.0 AI エージェントフレームワークなど多数発表 | [JetBrains Blog](https://blog.jetbrains.com/kotlin/2026/05/kotlinconf26-keynote-highlights/) |
| 2 | Next.js / React | セキュリティリリース (13 CVE) | Next.js 11件 + React Server Components 1件 + フォローアップ1件の計13件のセキュリティアドバイザリを修正。DoS・SSRF・XSS・キャッシュポイズニング等。15.5.18 / 16.2.6 へのアップグレード推奨 | [Vercel Changelog](https://vercel.com/changelog/next-js-may-2026-security-release) |
| 3 | pnpm | 11.2 リリース | 実験的に pacquet（pnpm の Rust ポート）をインストールバックエンドとして利用可能に。config dependencies の optionalDependencies 対応、`pnpm login --scope` の実装 | [pnpm Blog](https://pnpm.io/blog/releases/11.2) |
| 4 | Vue.js | 3.6 Vapor Mode Beta | Virtual DOM を完全に排除する Vapor Mode が feature-complete で Beta に。10万コンポーネントを約100msでマウント、Solid/Svelte 5 同等のベンチマーク性能 | [GitHub Release](https://github.com/vuejs/core/releases/tag/v3.6.0-beta.1) |
| 5 | Python | 3.15.0b1 (Beta 開始) | Python 3.15 が Beta フェーズに突入（5月5日）。これ以降の新機能追加は凍結。正式リリースは 2026年10月予定 | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/) |
| 6 | Go | 1.25.10 / 1.26.3 セキュリティリリース | go コマンド、html/template、net/http 等のセキュリティ修正。コンパイラ・リンカ・ランタイムのバグ修正も含む | [Go Release History](https://go.dev/doc/devel/release) |
| 7 | PostgreSQL | 18.4 メンテナンスリリース | PostgreSQL 18 系の4回目のメンテナンスリリース。17.10、16.14 等の旧バージョンも同時リリース | [PostgreSQL News](https://www.postgresql.org/about/newsarchive/) |
| 8 | Svelte | 5.55.0 / SvelteKit 更新 | リモート関数の hydratable トランスポート対応、フォームの default value 指定、TypeScript 6.0 サポート。CLI にコミュニティアドオンの実験的サポート追加 | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-may-2026) |
| 9 | IntelliJ IDEA | 2026.1.2 バグ修正リリース | 2026.1 系のパッチリリース。AI エージェント統合（Codex, Cursor, ACP 対応）、Git worktree、Kotlin 2.3.20 サポート等を含む 2026.1 ベースの安定化 | [JetBrains Blog](https://blog.jetbrains.com/idea/2026/05/intellij-idea-2026-1-2/) |
| 10 | React | 19.2.6 リリース | 型のハードニングとパフォーマンス改善。Next.js セキュリティリリースと同日の協調リリースで、react-server-dom-* パッケージの脆弱性も修正 | [GitHub Releases](https://github.com/facebook/react/releases) |

## Deep Dive

- [KotlinConf 2026 — Kotlin 2.4 プレビュー・VS Code Alpha・Exposed 1.0](./tu-kotlinconf-2026.md)
- [Next.js / React May 2026 セキュリティリリース — 13 CVE の全容](./tu-nextjs-react-security-may-2026.md)
