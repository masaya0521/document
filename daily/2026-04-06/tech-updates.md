# Tech Updates — 2026-04-06

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Vite | v8.0 リリース | Rust ベースの Rolldown を統一バンドラーとして採用。ビルド速度 10-30 倍向上、DevTools 統合、WASM SSR サポート | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 2 | TypeScript | v6.0 リリース | JS ベース最終リリース。strict デフォルト化、Temporal API サポート、ES2025 ターゲット、インクリメンタルビルド 40-60% 高速化 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 3 | Tailwind CSS | v4.2.0 / v4.2.2 リリース | 新カラーパレット4種（mauve, olive, mist, taupe）、公式 Webpack プラグイン、論理プロパティユーティリティ、Vite 8 サポート | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases/tag/v4.2.2) |
| 4 | JetBrains IDE | 2026.1 一斉リリース | IntelliJ IDEA / GoLand / WebStorm / PhpStorm 等。ACP エージェント統合、Git worktree サポート、各言語固有の改善 | [IntelliJ IDEA Blog](https://blog.jetbrains.com/idea/2026/03/intellij-idea-2026-1/) |
| 5 | ReSharper | VS Code 拡張 GA リリース | 1年間のパブリックプレビューを経て正式リリース。VS Code / Cursor / Antigravity で C# コード解析・リファクタリングが利用可能に | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 6 | Astro | v6 Beta | Cloudflare Workers ファーストクラスサポート、開発サーバー刷新（本番と同一ランタイム）、CSP / フォント / コンテンツコレクション新 API | [Astro Blog](https://astro.build/blog/astro-6-beta/) |
| 7 | GitHub Actions | 2026年4月初旬アップデート | サービスコンテナの entrypoint/command オーバーライド、OIDC カスタムプロパティ、Azure プライベートネットワークフェイルオーバー | [GitHub Changelog](https://github.blog/changelog/2026-04-02-github-actions-early-april-2026-updates/) |
| 8 | GoLand | 2026.1 リリース | Go 1.26 ガイド付きシンタックス更新、Terraform Stacks サポート、Git worktree サポート、AI エージェント統合 | [GoLand Blog](https://blog.jetbrains.com/go/2026/03/26/goland-2026-1-is-released/) |
| 9 | ReSharper | 2026.1 リリース | ビルトインパフォーマンスモニタリング（CPU・メモリ割当の可視化）、VS Code 展開強化、日常ワークフロー高速化 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/30/resharper-2026-1-released/) |
| 10 | Actions Runner Controller | v0.14.0 リリース | GitHub Actions セルフホストランナーの Kubernetes コントローラー更新 | [GitHub Changelog](https://github.blog/changelog/2026-03-19-actions-runner-controller-release-0-14-0/) |

## Deep Dive

- [Vite 8.0 — Rolldown 統一バンドラーによるアーキテクチャ刷新](./tu-vite-8-rolldown.md)
