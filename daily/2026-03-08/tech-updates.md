# Tech Updates — 2026-03-08

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 RC リリース | JavaScript ベース最後のリリース。Go ベースの TypeScript 7.0 への移行を支援する `--stableTypeOrdering` フラグを追加 | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/) |
| 2 | VS Code | 1.110 (February 2026) リリース | エージェントプラグイン、エージェント用ブラウザツール、セッションメモリ、コンテキストコンパクション、チャットセッションのフォーク機能を追加 | [VS Code Updates](https://code.visualstudio.com/updates/v1_110) |
| 3 | GitHub Copilot | コードレビューがエージェントアーキテクチャに移行・GA | エージェント型ツールコールでリポジトリ全体のコンテキストを収集し、より高品質なレビューフィードバックを提供 | [GitHub Changelog](https://github.blog/changelog/2026-03-05-copilot-code-review-now-runs-on-an-agentic-architecture/) |
| 4 | JetBrains ReSharper | VS Code / Cursor 向け拡張が正式リリース | 1年間のパブリックプレビューを経て GA。C# コード解析・リファクタリング・フォーマット機能を VS Code エコシステムに提供。非商用利用は無料 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 5 | Astro | 6 Beta | Cloudflare による買収後初のメジャーリリースベータ。Vite Environment API、Workerd 開発サーバー、CSP・フォント・ライブコンテンツコレクションの組み込み API を追加 | [Astro Blog](https://astro.build/blog/astro-6-beta/) |
| 6 | pnpm | 11.0.0-alpha.12 | グローバルインストールがグローバル仮想ストアをデフォルト使用、パッケージごとの分離インストール、信頼ポリシー（trustPolicy）の追加 | [GitHub Releases](https://github.com/pnpm/pnpm/releases) |
| 7 | React Router | v7 安定版 (Remix 統合) | Remix v3 が React Router v7 として統合リリース。Declarative / Data / Framework の3モードを提供。1月にはCSRF・XSS等のセキュリティ修正も実施 | [Remix Blog](https://remix.run/blog/react-router-v7) |
| 8 | GitHub Copilot | メトリクスにプランモード追加 | エンタープライズ向けにプランモードの採用・エンゲージメント追跡が可能に | [GitHub Changelog](https://github.blog/changelog/2026-03-02-copilot-metrics-now-includes-plan-mode/) |
| 9 | Google LiteRT | TFLite 後継として正式ローンチ | GPU/NPU アクセラレーションの大幅高速化、PyTorch・JAX のシームレスサポート、低精度データ型による効率化 | [Google Developers Blog](https://developers.googleblog.com/) |
| 10 | Rust | 1.85-1.94 安定版 (最新 1.94.0) | 安定版 1.94.0 がリリース済み。次期ベータ 1.95.0 は 2026年4月16日予定 | [Rust Releases](https://releases.rs/) |

## Deep Dive

- [TypeScript 6.0 RC — JavaScript ベース最後のリリースと Go ベース TypeScript 7.0 への移行](./tu-typescript-6-rc.md)
- [VS Code 1.110 — エージェント機能の本格化](./tu-vscode-1-110.md)
