# Tech Updates — 2026-03-30

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Vite | v8.0 リリース | Rolldown（Rust 製バンドラー）に統一。esbuild + Rollup の二重構成を廃止し、10〜30x 高速化を実現 | [Vite Blog](https://vite.dev/blog/announcing-vite8) |
| 2 | TypeScript | v6.0 リリース | JS ベース最終リリース。Go ネイティブの v7.0 への橋渡しとして多数のデフォルト変更・非推奨化を実施 | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 3 | JDK | 26 GA | HTTP/3 対応、AOT キャッシュの GC 非依存化、G1 GC スループット向上、Applet API 完全削除 | [Oracle](https://www.oracle.com/news/announcement/oracle-releases-java-26-2026-03-17/) |
| 4 | Rust | v1.94.0 リリース | array_windows 安定化、AVX-512 FP16 / AArch64 NEON FP16 intrinsics 安定化、Cargo の TOML 1.1 対応 | [Rust Blog](https://blog.rust-lang.org/2026/03/05/Rust-1.94.0/) |
| 5 | VS Code | v1.113 リリース | AI 思考レベル調整、ネストサブエージェント、CLI エージェント機能、デフォルトテーマ刷新 | [VS Code](https://code.visualstudio.com/updates/v1_113) |
| 6 | JetBrains | 2026.1 一斉リリース | IntelliJ IDEA・GoLand・PhpStorm・CLion 等。ACP レジストリ、Git worktree 対応、AI エージェント連携強化 | [JetBrains Blog](https://blog.jetbrains.com/idea/2026/03/intellij-idea-2026-1/) |
| 7 | ReSharper | VS Code 版正式リリース | 1年間のパブリックプレビューを経て正式版に。Cursor・Google Antigravity 等の AI エディタにも対応 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 8 | Tailwind CSS | v4.2.2 リリース | Vite 8 公式サポート追加 | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases) |
| 9 | Go | v1.25.8 セキュリティリリース | html/template・net/url・os パッケージのセキュリティ修正 | [Go Release History](https://go.dev/doc/devel/release) |
| 10 | GitHub | REST API v2026-03-10 | 新 API バージョン公開。破壊的変更あり（旧 v2022-11-28 は 24 ヶ月間継続サポート） | [GitHub Changelog](https://github.blog/changelog/2026-03-12-rest-api-version-2026-03-10-is-now-available/) |

## Deep Dive

- [Vite 8.0 — Rolldown による統一バンドラーへの移行](./tu-vite-8-rolldown.md)
- [TypeScript 6.0 — Go ネイティブ 7.0 への橋渡しリリース](./tu-typescript-6-0.md)
