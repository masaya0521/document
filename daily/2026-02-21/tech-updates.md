# Tech Updates — 2026-02-21

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 Beta (Feb 11) | JS ベースコンパイラの最終バージョン。strict デフォルト true 化、ES2025/Temporal 対応、多数の非推奨オプション追加で TS 7.0（Go ベース）への移行を準備 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/) |
| 2 | Vite | 8.0 Beta (beta.15: Feb 19) | Rolldown（Rust 製バンドラー）に統一。esbuild + Rollup の二重構成を廃止し、ビルド 10-30x 高速化。Linear は 46s→6s に短縮 | [公式ブログ](https://vite.dev/blog/announcing-vite8-beta) |
| 3 | Tailwind CSS | 4.2 リリース | @tailwindcss/webpack パッケージ追加、block/inline 論理プロパティユーティリティ群の新設、start-*/end-* の非推奨化 | [GitHub](https://github.com/tailwindlabs/tailwindcss/releases) |
| 4 | Astro | 6.0 Beta (継続中) | 開発サーバーを Vite Environment API で刷新し dev/prod の一致性を向上。CSP・Fonts API 安定化、Node 22 必須化 | [公式ブログ](https://astro.build/blog/astro-6-beta/) |
| 5 | PostgreSQL | 18.3/17.9 等 臨時リリース (Feb 26 予定) | 18.2 で導入された substring() リグレッション（CVE-2026-2006 修正起因）とスタンバイエラーの修正 | [公式](https://www.postgresql.org/about/news/out-of-cycle-release-scheduled-for-february-26-2026-3241/) |
| 6 | Rust | 1.93.1 (Feb 12) | rustfmt の ICE バグ修正（キーワード回復処理）と clippy の panicking_unwrap 偽陽性修正 | [公式ブログ](https://blog.rust-lang.org/2026/02/12/Rust-1.93.1/) |
| 7 | SvelteKit | adapter-node 5.5.0 / adapter-vercel 6.3.1 | Node: keepAliveTimeout/headersTimeout の環境変数設定対応。Vercel: remote function の /_app/remote ルート対応。エコシステム全体で 5 件の脆弱性修正 | [公式ブログ](https://svelte.dev/blog/whats-new-in-svelte-february-2026) |
| 8 | Visual Studio 2026 | v18.3.1 (Feb 18) | MSVC Build Tools 14.51 Preview、IDE 内カスタムプロキシ設定機能、デバッグ時変数ホバー表示の修正 | [リリースノート](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 9 | GitHub Copilot for JetBrains | Agent Skills パブリックプレビュー | .github/skills/ に SKILL.md を配置してエージェントに手続き的知識を付与。Cursor・Junie とも互換性のあるオープン標準として展開 | [GitHub Docs](https://docs.github.com/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide) |
| 10 | Django | 6.0.2 (Feb 3) | 6.0 系のバグ修正リリース | [公式](https://www.djangoproject.com/weblog/2026/) |

## Deep Dive

- [TypeScript 6.0 Beta — JS コンパイラ最終版の全貌](./tu-typescript-6-0-beta.md)
- [Vite 8.0 Beta — Rolldown 統合による次世代ビルド](./tu-vite-8-beta.md)
