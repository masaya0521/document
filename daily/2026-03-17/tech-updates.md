# Tech Updates — 2026-03-17

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 GA リリース | JS ベース最後のメジャーリリース。strict デフォルト化、ES2025 対応（Temporal, RegExp.escape）、非推奨オプション整理。次期 7.0 は Go ベースへ | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/) |
| 2 | Vite | 8.0 リリース | Rolldown（Rust 製バンドラー）を統合し dev/prod を単一バンドラーに統一。10-30x のビルド高速化（Linear: 46s→6s）。Vite Devtools 標準搭載 | [Vite Blog](https://vite.dev/blog/announcing-vite8) |
| 3 | Visual Studio | 2026 GA アップデート (3/10) | AI ネイティブ IDE。Copilot Agent Skills、Profiler Agent、Debugger Agent を搭載。リッチクリップボード対応、JSON Schema 最新仕様サポート | [Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 4 | ReSharper | VS Code 正式版リリース (3/5) | 1年のパブリックプレビューを経て正式版。C# コード解析・リファクタリングを VS Code / Cursor / Antigravity で利用可能。非商用は無料 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 5 | Go | 1.26.1 セキュリティ修正 (3/5) | crypto/x509, html/template, net/url, os パッケージのセキュリティ修正。Go 1.26 では Green Tea GC がデフォルト有効化、cgo オーバーヘッド約30%削減 | [Go Release History](https://go.dev/doc/devel/release) |
| 6 | Cursor | ACP で JetBrains IDE 対応 (3/4) | Agent Client Protocol を通じて IntelliJ IDEA, PyCharm, WebStorm 等で Cursor のエージェント機能を利用可能に。有料プランユーザーは追加料金なし | [Cursor Blog](https://cursor.com/blog/jetbrains-acp) |
| 7 | Atlassian | Jira/Confluence REST API クォータ制限施行開始 (3/2) | ポイントベースのクォータレート制限を段階的に施行開始。少数のアプリから開始し数週間かけて拡大。API 利用量の見直しが必要 | [Atlassian Changelog](https://developer.atlassian.com/changelog/) |
| 8 | Astro | 6 Beta — Cloudflare Workers ネイティブ対応 | Vite Environment API ベースの新 dev サーバー、workerd ランタイムでの開発、ライブコンテンツコレクション、CSP サポート。Node 22+ 必須 | [Astro Blog](https://astro.build/blog/astro-6-beta/) |
| 9 | @vitejs/plugin-react | v6 — Babel 依存を廃止、Oxc 採用 | Vite 8 に合わせて React プラグインを刷新。Babel を Oxc に置き換えインストールサイズを大幅縮小。JSX トランスフォームの高速化 | [Vite Blog](https://vite.dev/blog/announcing-vite8) |
| 10 | Tailwind CSS | @tailwindcss/vite が Vite 8 対応 (3/12) | Vite 8 リリース当日にピア依存を ^8.0.0 に拡張。統合テスト追加で互換性を確認。最新安定版は v4.2.1（2/23 リリース） | [Benjamin Crozat](https://benjamincrozat.com/tailwind-css-vite-8-support) |

## Deep Dive

- [TypeScript 6.0 GA — JS ベース最後のメジャーリリース](./tu-typescript-6-0.md)
- [Vite 8.0 — Rolldown 統合で 10-30x 高速化](./tu-vite-8-0.md)
