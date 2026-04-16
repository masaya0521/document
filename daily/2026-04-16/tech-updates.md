# Tech Updates — 2026-04-16

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | VS Code | v1.115 リリース (April 3) | 新しい VS Code Agents コンパニオンアプリ、Copilot Business/Enterprise 向け BYOK 対応、統合ブラウザ・ターミナルの改善 | [Release Notes](https://code.visualstudio.com/updates/v1_115) |
| 2 | .NET Framework | April 2026 セキュリティ更新 (April 14) | CVE-2026-32178（RCE）、CVE-2026-32203（DoS）等の脆弱性修正を含む累積更新プログラム | [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/framework/release-notes/2026/04-14-april-cumulative-update) |
| 3 | Next.js | v16.2 → 16.2.3 LTS | dev サーバー起動が約 400% 高速化、Turbopack で Server Fast Refresh・200+ バグ修正、AI 向け AGENTS.md 対応 | [Releasebot](https://releasebot.io/updates/vercel/next-js) |
| 4 | TypeScript | v6.0 リリース (March 23) | JS ベース最後のリリース。strict デフォルト化、ES2025 ターゲット、Temporal 型追加。Go ネイティブ v7.0 への橋渡し | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 5 | Vite | v8.0 リリース (March 12) | Rolldown（Rust 製バンドラー）ベースのアーキテクチャ刷新。esbuild + Rollup を統一し 10-30x 高速化 | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 6 | JetBrains IDE | 2026.1 リリース (March 30) | IntelliJ IDEA で JS/TS 無料サポート、WebStorm で TypeScript エンジン刷新、全 IDE で ACP エージェント対応 | [IntelliJ Blog](https://blog.jetbrains.com/idea/2026/03/intellij-idea-2026-1/) |
| 7 | ReSharper | VS Code 拡張 正式リリース (March 5) | 1年の Public Preview を経て VS Code・Cursor 等の互換エディタに C# コード解析・生産性機能を提供 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 8 | Tailwind CSS | v4.2 リリース (February 18) | @tailwindcss/webpack プラグイン追加、4つの新カラーパレット、論理プロパティユーティリティ、再コンパイル 3.8x 高速化 | [InfoQ](https://www.infoq.com/news/2026/04/tailwind-css-4-2-webpack/) |
| 9 | Vue.js | v3.6 beta (Vapor Mode) | 仮想 DOM を排除し直接 DOM 操作にコンパイル。10万コンポーネントを約100msでマウント、SolidJS と同等のパフォーマンス | [Vue School](https://vueschool.io/articles/news/vn-talk-evan-you-preview-of-vue-3-6-vapor-mode/) |
| 10 | Deno | 最新リリース (April 9) | マルチプラットフォーム対応の最新バイナリ配布。Node.js 互換性の継続的改善 | [GitHub Releases](https://github.com/denoland/deno/releases) |

## Deep Dive

- [TypeScript 6.0 — Go ネイティブ 7.0 への橋渡しリリース](./tu-typescript-6-0.md)
- [Vite 8.0 — Rolldown による Rust ベースアーキテクチャ刷新](./tu-vite-8-rolldown.md)
