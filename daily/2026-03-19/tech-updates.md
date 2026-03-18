# Tech Updates — 2026-03-19

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 GA リリース | JS ベース最後のメジャーリリース。Go ベースの TS 7.0 への橋渡しとして、strict デフォルト化・es2025 target・Temporal API 型サポート・多数の非推奨化を含む | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/) |
| 2 | Vite | 8.0 リリース | Rust 製バンドラー Rolldown を単一バンドラーとして統合。ビルド速度 10-30x 向上、DevTools 組み込み、Wasm SSR 対応 | [Vite Blog](https://vite.dev/blog/announcing-vite8) |
| 3 | Next.js | 16.2 リリース | dev 起動 87% 高速化、Server Components デシリアライズ最大 350% 高速化、View Transitions、Turbopack 200+ 修正 | [Next.js Blog](https://nextjs.org/blog/next-16-2) |
| 4 | VS Code | 1.111（週次リリース開始） | 月次→週次リリースに移行。Autopilot モード（Preview）、Agent Permissions、Agent-scoped Hooks を追加 | [VS Code Updates](https://code.visualstudio.com/updates/v1_111) |
| 5 | ReSharper for VS Code | GA リリース | JetBrains が ReSharper 拡張を VS Code / Cursor / Antigravity 向けに正式リリース。非商用利用は無料 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 6 | Visual Studio | 2026 GA | AI ネイティブ IDE として正式リリース。5,000 以上のバグ修正、Copilot Agents のスキル自動検出、HTML クリップボード対応 | [Visual Studio Blog](https://devblogs.microsoft.com/visualstudio/visual-studio-2026-is-here-faster-smarter-and-a-hit-with-early-adopters/) |
| 7 | WordPress | 7.0 RC1 | リアルタイムコラボレーション機能を含む WordPress 7.0 の RC1。正式リリースは 4/9 予定 | [WordPress News](https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/) |
| 8 | .NET | 10.0.4 / 9.0.14 / 8.0.25 サービシング | 2 件の CVE（CVE-2026-26127, CVE-2026-26131）対応を含むセキュリティ & 非セキュリティ修正 | [.NET Blog](https://devblogs.microsoft.com/dotnet/dotnet-and-dotnet-framework-march-2026-servicing-updates/) |
| 9 | SQL Server 2022 | CU24 | 15 件の修正を含む累積更新プログラム（3/12 リリース） | [Microsoft Learn](https://learn.microsoft.com/en-us/troubleshoot/sql/releases/sqlserver-2022/cumulativeupdate24) |
| 10 | Tailwind CSS | Vite 8 対応 | Vite 8.0 リリース当日に @tailwindcss/vite の peer dependency を ^8.0.0 に拡張、統合テスト追加 | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases) |

## Deep Dive

- [TypeScript 6.0 — JS ベース最後のメジャーリリースと Go リライトへの移行準備](./tu-typescript-6-0.md)
- [Vite 8.0 — Rolldown 統合による 10-30x 高速化とアーキテクチャ刷新](./tu-vite-8-0-rolldown.md)
