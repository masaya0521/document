# Tech Updates — 2026-03-24

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | v6.0 正式リリース | JS ベース最終版。Temporal API サポート、strict デフォルト true 化、ES5 出力廃止。Go ベースの v7.0 への橋渡し | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 2 | Vite | v8.0 リリース | Rust 製統一バンドラー Rolldown を採用。esbuild + Rollup の二重構成を廃止し、10-30x 高速化を実現 | [Vite Blog](https://vite.dev/blog/announcing-vite8) |
| 3 | VS Code | v1.112 + 週次リリース移行 | 3/9 から週次リリースに移行。v1.112 で統合ブラウザデバッガー、MCP サーバーサンドボックス、Autopilot プレビュー | [GitHub Issue](https://github.com/microsoft/vscode/issues/300108) |
| 4 | Tailwind CSS | v4.2.2 | Vite 8 の公式サポートを追加。Rolldown バンドラーとの互換性を確保 | [npm](https://www.npmjs.com/package/@tailwindcss/vite) |
| 5 | Go | v1.26.1 セキュリティ修正 | crypto/x509、html/template、net/url、os パッケージのセキュリティ修正とコンパイラバグ修正 | [Go Release History](https://go.dev/doc/devel/release) |
| 6 | .NET | 10.0.4 / 9.0.14 / 8.0.25 | CVE-2026-26127（ランタイム DoS）、CVE-2026-26130（ASP.NET Core DoS）の修正 | [.NET Blog](https://devblogs.microsoft.com/dotnet/dotnet-and-dotnet-framework-march-2026-servicing-updates/) |
| 7 | Visual Studio | 2026 March アップデート | C++ Code Editing Tools for Copilot Agent Mode がデフォルト有効に。JSON エディタがコアに統合 | [Release Notes](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 8 | Deno | v2.7.6 | Node.js 互換性の修正、プロセス管理の改善、WebIDL 最適化 | [GitHub Releases](https://github.com/denoland/deno/releases) |
| 9 | GitHub Copilot for JetBrains | エージェント機能 GA | カスタムエージェント、サブエージェント、プランエージェントが GA。拡張推論モデル用の thinking パネル追加 | [GitHub Changelog](https://github.blog/changelog/2026-03-11-major-agentic-capabilities-improvements-in-github-copilot-for-jetbrains-ides/) |
| 10 | C++26 | フィーチャーフリーズ（WG21 ロンドン会議） | 3/23-28 の WG21 会議で C++26 がフィーチャーコンプリート。static reflection、contracts、std::execution、SIMD 型、parallel Ranges を含む | [devnewsletter](https://devnewsletter.com/p/state-of-cpp-2026/) |

## Deep Dive

- [TypeScript 6.0 — JS ベース最終リリースと v7.0 への移行](./tu-typescript-6-0.md)
- [Vite 8.0 — Rolldown による統一バンドラーアーキテクチャ](./tu-vite-8-0.md)
