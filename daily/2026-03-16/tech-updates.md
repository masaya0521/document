# Tech Updates — 2026-03-16

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Vite | 8.0 リリース | Rust ベースバンドラー Rolldown に統一。ビルド速度 10〜30 倍向上、Linear では 46s→6s に短縮 | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 2 | TypeScript | 6.0 RC | JS ベース最後のリリース。Temporal API 対応、strict デフォルト化、ES5/AMD/UMD 出力削除 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/) |
| 3 | VS Code | 1.111（週次リリース化） | 月次から週次リリースへ移行。Autopilot モード（プレビュー）、エージェント権限設定を追加 | [リリースノート](https://code.visualstudio.com/updates/v1_111) |
| 4 | Visual Studio | 2026 March アップデート | JSON Schema サポート強化（$defs, $anchor 対応）、Copilot Agent Skills の自動検出 | [リリースノート](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 5 | GitHub Copilot | JetBrains エージェント機能 GA | カスタムエージェント・サブエージェント・プランエージェントが GA。MCP の自動承認、AGENTS.md 対応 | [GitHub Changelog](https://github.blog/changelog/2026-03-11-major-agentic-capabilities-improvements-in-github-copilot-for-jetbrains-ides/) |
| 6 | .NET | 10.0.4 / 9.0.14 / 8.0.25 | セキュリティアップデート。CVE-2026-26127（DoS）、CVE-2026-26131 を修正 | [.NET Blog](https://devblogs.microsoft.com/dotnet/dotnet-and-dotnet-framework-march-2026-servicing-updates/) |
| 7 | @vitejs/plugin-react | v6 リリース | React Refresh の変換に Oxc を採用、Babel 依存を完全削除 | [GitHub Releases](https://github.com/vitejs/vite/releases) |
| 8 | Go | 1.26.1 セキュリティパッチ | crypto/x509, html/template, net/url, os パッケージのセキュリティ修正 | [Go Release History](https://go.dev/doc/devel/release) |
| 9 | GitHub Copilot | Code Review エージェントアーキテクチャ化 | コードレビュー機能がエージェントアーキテクチャ上で動作するよう刷新 | [GitHub Changelog](https://github.blog/changelog/2026-03-05-copilot-code-review-now-runs-on-an-agentic-architecture/) |
| 10 | Python | 3.11.15 / 3.10.20 | セキュリティメンテナンスリリース（3月3日） | [Python.org](https://www.python.org/doc/versions/) |

## Deep Dive

- [Vite 8.0 — Rolldown 統合による次世代ビルド](./tu-vite-8.md)
- [TypeScript 6.0 RC — JS ベース最後のリリースと移行ガイド](./tu-typescript-6-rc.md)
