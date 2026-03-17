# Tech Updates — 2026-03-18

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 GA リリース | JavaScript ベース最後のメジャーリリース。`strict: true` デフォルト化、Temporal API 型、`RegExp.escape()` 追加。次の 7.0 は Go ベースへ移行 | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/) |
| 2 | Vite | 8.0 リリース | Rust 製バンドラー Rolldown に統一。ビルド速度 10-30 倍高速化（Linear: 46s→6s）。統合 Devtools、Wasm SSR サポート追加 | [Vite Blog](https://vite.dev/blog/announcing-vite8) |
| 3 | Go | 1.26.1 セキュリティリリース | crypto/x509、html/template、net/url、os の 5 件の CVE を修正。XSS リスクや証明書検証の問題に対応 | [golang-announce](https://groups.google.com/g/golang-announce/c/EdhZqrQ98hk/m/41DopX_WAAAJ) |
| 4 | VS Code | 1.111（週次リリース開始） | 月次から週次 Stable リリースへ移行。エージェント権限管理、エージェントスコープフック、デバッグ機能強化 | [GitHub Release](https://github.com/microsoft/vscode/releases/tag/1.111.0) |
| 5 | .NET | 10.0.4 / 9.0.14 / 8.0.25 サービシング更新 | CVE-2026-26127、CVE-2026-26130、CVE-2026-26131 を修正。ASP.NET Core、EF Core、WPF 等のセキュリティ・バグ修正 | [.NET Blog](https://devblogs.microsoft.com/dotnet/dotnet-and-dotnet-framework-march-2026-servicing-updates/) |
| 6 | Svelte | March 2026 アップデート | `createContext` サポート、TrustedHTML 対応、サーバーサイドエラーバウンダリ追加。SvelteKit の Netlify Adapter 刷新 | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-march-2026) |
| 7 | ReSharper for VS Code | 正式リリース | 1 年の Public Preview を経て VS Code / Cursor / 互換エディタ向けに正式版をリリース。非商用利用は無料。Open VSX Registry にも公開 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 8 | Tailwind CSS | @tailwindcss/vite Vite 8 対応 | Vite 8 リリースに合わせて `@tailwindcss/vite` の peer dependency を `^8.0.0` に拡張。v4.2.1 が最新安定版 | [GitHub PR #19790](https://github.com/tailwindlabs/tailwindcss/pull/19790) |
| 9 | Nuxt | 4.4.2 リリース | Vue フレームワーク Nuxt の最新パッチリリース（2026-03-12） | [Nuxt EOL Info](https://eosl.date/eol/product/nuxt/) |
| 10 | Python | 3.10.20 リリース | セキュリティメンテナンスリリース（2026-03-03）。Python 3.10 系の継続サポート | [Python.org](https://www.python.org/doc/versions/) |

## Deep Dive

- [Vite 8.0 — Rolldown 統合によるビルド革命](./tu-vite-8-rolldown.md)
- [TypeScript 6.0 — JavaScript ベース最後のリリースと Go 移行への布石](./tu-typescript-6-0.md)
