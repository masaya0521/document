# Tech Updates — 2026-04-05

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Vite | v8.0 リリース | Rust 製バンドラー Rolldown を統合し、ビルド速度 10-30x 高速化。esbuild + Rollup の二重構成を廃止し単一バンドラーに統一 | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 2 | Next.js | v16.2 リリース | `next dev` 起動が約 87% 高速化、Server Components レンダリングが最大 60% 改善。新デフォルトエラーページ、Turbopack 200 以上のバグ修正 | [公式ブログ](https://nextjs.org/blog/next-16-2) |
| 3 | Astro | v6.0 stable リリース | 組み込み Fonts API、Content Security Policy API、Live Content Collections を追加。Cloudflare Workers での開発サーバー実行に対応 | [公式ブログ](https://astro.build/blog/astro-6/) |
| 4 | JetBrains IDE | 2026.1 リリース | IntelliJ IDEA, PyCharm, GoLand, PhpStorm 等の全 IDE で 2026.1 をリリース。ACP Registry による AI エージェント統合、Git worktree 対応 | [IntelliJ IDEA ブログ](https://blog.jetbrains.com/idea/2026/03/intellij-idea-2026-1/) |
| 5 | VS Code | v1.111 — 週次リリース開始 | 月次から週次リリースに移行。Autopilot（プレビュー）でエージェントが自律的にタスクを完了、エージェント権限設定を追加 | [リリースノート](https://code.visualstudio.com/updates/v1_111) |
| 6 | VS Code | v1.112 リリース | 統合ブラウザデバッグ、MCP サーバーサンドボックス、エージェント画像サポート、モノレポ向けエージェント設定カスタマイズ | [リリースノート](https://code.visualstudio.com/updates/v1_112) |
| 7 | Tailwind CSS | v4.2.0 リリース | 公式 Webpack プラグイン追加、4 つの新カラーパレット（mauve, olive, mist, taupe）、論理プロパティユーティリティの拡充 | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases) |
| 8 | Go | v1.26 リリース + v1.26.1 パッチ | Green Tea GC がデフォルト有効化、crypto/hpke パッケージ追加（RFC 9180）。v1.26.1 でセキュリティ修正 | [公式ブログ](https://go.dev/blog/go1.26) |
| 9 | ReSharper | 2026.1 — VS Code 対応 | ReSharper の C# ツーリングが VS Code、Cursor、Google Antigravity で利用可能に。ランタイムパフォーマンスモニタリング機能を追加 | [JetBrains ブログ](https://blog.jetbrains.com/dotnet/2026/03/30/resharper-2026-1-released/) |
| 10 | pnpm | v11 beta | グローバルインストールが仮想ストアをデフォルト使用、インデックスファイル形式の最適化、ライフサイクルスクリプト実行のセキュリティ強化 | [GitHub Releases](https://github.com/pnpm/pnpm/releases) |

## Deep Dive

- [Vite 8.0 — Rolldown 統合で JavaScript ビルドツールの新時代へ](./tu-vite-8-rolldown.md)
