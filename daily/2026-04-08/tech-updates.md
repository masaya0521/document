# Tech Updates — 2026-04-08

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 正式リリース | JavaScript ベースコンパイラ最終版。strict デフォルト化、ES2025 ターゲット、Temporal 型追加。Go ベース TypeScript 7.0 への移行準備 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 2 | Vite | 8.0 リリース | Rolldown（Rust 製バンドラ）を統合し esbuild・Rollup を置換。ビルド速度 10-30x 向上、Full Bundle Mode（実験的）で dev 起動 3x 高速化 | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 3 | Astro | 6.0 安定版リリース | Vite Environment API による開発・本番ランタイム統一、Cloudflare Workers ファーストクラスサポート、Fonts API・CSP API・Live Content Collections 追加 | [公式ブログ](https://astro.build/blog/astro-6/) |
| 4 | WebStorm | 2026.1 リリース | TypeScript 6 対応、サービスベース TypeScript エンジンをデフォルト化、Junie・Claude Agent・Codex 等の AI エージェント統合、Angular 21 テンプレート対応 | [JetBrains ブログ](https://blog.jetbrains.com/webstorm/2026/03/webstorm-2026-1/) |
| 5 | IntelliJ IDEA | 2026.1 リリース | Codex・Cursor 等 ACP 対応 AI エージェント統合、Java・Kotlin・Spring 向け改善、JavaScript/TypeScript の基本サポートを無料版にも提供 | [JetBrains ブログ](https://blog.jetbrains.com/idea/2026/03/intellij-idea-2026-1/) |
| 6 | ReSharper | 2026.1 リリース | VS Code・Cursor 対応（VS 外での C# ツーリング）、パフォーマンスモニタリング機能内蔵、ソリューションインデックス・コード補完の高速化 | [JetBrains ブログ](https://blog.jetbrains.com/dotnet/2026/03/30/resharper-2026-1-released/) |
| 7 | Tailwind CSS | 4.2 リリース | webpack プラグイン（@tailwindcss/webpack）追加、新カラーパレット 4 種（mauve, olive, mist, taupe）、論理プロパティユーティリティ拡充 | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases) |
| 8 | GitHub Actions | Early April 2026 アップデート | サービスコンテナの entrypoint/command オーバーライド、OIDC トークンにリポジトリカスタムプロパティ追加、Azure VNET フェイルオーバー対応 | [GitHub Changelog](https://github.blog/changelog/2026-04-02-github-actions-early-april-2026-updates/) |
| 9 | GitHub Copilot | コーディングエージェント管理 REST API | Organization オーナーがリポジトリアクセスをプログラマティックに制御可能に（パブリックプレビュー）。Jira 連携強化、Confluence MCP 対応 | [GitHub Changelog](https://github.blog/changelog/) |
| 10 | Redis Enterprise for K8s | 8.0.16-25 リリース | OSS Cluster API の外部クライアント対応、ARM アーキテクチャサポート、Redis Software 8.0.16-64 ベース | [Redis Docs](https://redis.io/docs/latest/operate/kubernetes/release-notes/8-0-16-releases/8-0-16-25-march2026/) |

## Deep Dive

- [TypeScript 6.0 — JavaScript ベースコンパイラ最終版と Go リライトへの道](./tu-typescript-6-0.md)
- [Vite 8.0 — Rolldown 統合によるアーキテクチャ刷新](./tu-vite-8-rolldown.md)
