# Tech Updates — 2026-04-14

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | VS Code | v1.115 リリース | VS Code Agents コンパニオンアプリ（プレビュー）を導入。複数リポジトリでエージェントセッションを並列実行可能に。BYOK 対応で Copilot Business/Enterprise ユーザーが外部 LLM を利用可能に | [Release Notes](https://code.visualstudio.com/updates/v1_115) |
| 2 | Slack CLI | v4.0.0 リリース | AI Agent 開発に特化した大型アップデート。`slack create agent` コマンドで AI エージェントをスキャフォールド可能。MCP Server をビルトインで搭載 | [Changelog](https://docs.slack.dev/changelog/2026/04/10/slack-cli/) |
| 3 | GitHub Copilot | cloud agent 検証ツール高速化 | CodeQL、シークレットスキャン、コードレビューの並列処理により検証ツールが20%高速化 | [GitHub Changelog](https://github.blog/changelog/2026-04-10-copilot-cloud-agents-validation-tools-are-now-20-faster/) |
| 4 | React Router | v7.14.0 リリース | Vite 8 対応、大規模ペイロードでの Turbo Stream のメモリリーク修正、unstable RSC Framework Mode でプリレンダリング・SPA 対応を拡張 | [GitHub Releases](https://github.com/remix-run/react-router/releases) |
| 5 | Vite | v8.0 リリース | Rust ベースの Rolldown バンドラーに統一。esbuild + Rollup の二重パイプラインを廃止し、ビルド速度 10-30 倍高速化を実現 | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 6 | Astro | v6.0 安定版リリース | Cloudflare Workers のファーストクラスサポート、Vite Environment API ベースの開発サーバー刷新、Fonts API・CSP 対応 | [公式ブログ](https://astro.build/blog/astro-6/) |
| 7 | JetBrains IDE | 2026.1 リリース | IntelliJ IDEA（Java 26 対応）、WebStorm（サービス駆動 TypeScript エンジン）、GoLand（Go 1.26 構文対応）が一斉リリース。ACP 経由で外部 AI エージェント統合 | [IntelliJ Blog](https://blog.jetbrains.com/idea/2026/03/intellij-idea-2026-1/) |
| 8 | Tailwind CSS | v4.2 リリース | webpack プラグイン（`@tailwindcss/webpack`）追加、新カラーパレット4種（mauve, olive, mist, taupe）、論理プロパティユーティリティ拡張、再コンパイル速度 3.8 倍改善 | [InfoQ](https://www.infoq.com/news/2026/04/tailwind-css-4-2-webpack/) |
| 9 | Vue.js | v3.6 beta（Vapor Mode） | 仮想 DOM を排除する Vapor Mode を導入。ビルド時にテンプレートを直接 DOM 操作にコンパイルし、SolidJS 並みのパフォーマンスを実現。10万コンポーネントを100msでマウント | [Vue School](https://vueschool.io/articles/news/vn-talk-evan-you-preview-of-vue-3-6-vapor-mode/) |
| 10 | GitHub Actions | 2026年4月初旬アップデート | サービスコンテナの entrypoint/command オーバーライド対応、OIDC カスタムプロパティ、VNET フェイルオーバーなどセキュリティ強化 | [GitHub Changelog](https://github.blog/changelog/2026-04-02-github-actions-early-april-2026-updates/) |

## Deep Dive

- [Vite 8.0 — Rolldown 統合による次世代ビルドツールチェーン](./tu-vite-8-rolldown.md)
- [VS Code 1.115 — エージェントネイティブ開発の幕開け](./tu-vscode-1-115-agents.md)
