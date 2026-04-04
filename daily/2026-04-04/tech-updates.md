# Tech Updates — 2026-04-04

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Vite | v8.0 リリース | Rolldown（Rustベースバンドラー）を統合し、ビルド速度 10〜30倍向上。esbuild + Rollup の二重構造を解消 | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 2 | Go | v1.26 リリース | Green Tea GC の正式有効化、cgo オーバーヘッド約30%削減、ゴルーチンリーク検出プロファイル追加 | [公式ブログ](https://go.dev/blog/go1.26) |
| 3 | VS Code | v1.114 リリース | 週次リリース体制での最新版。TypeScript 6.0 対応、チャット体験の改善、エンタープライズポリシー制御追加 | [リリースノート](https://code.visualstudio.com/updates/v1_114) |
| 4 | JetBrains | 2026.1 一斉リリース | GoLand・PhpStorm・ReSharper 等が 2026.1 をリリース。Git worktree サポート、MCP ツール統合、Code With Me のアンバンドル | [GoLand](https://blog.jetbrains.com/go/2026/03/26/goland-2026-1-is-released/), [PhpStorm](https://blog.jetbrains.com/phpstorm/2026/03/phpstorm-2026-1-is-now-out/) |
| 5 | ReSharper | VS Code 対応版 正式リリース | ReSharper の C# ツーリングが VS Code・Cursor・Google Antigravity で利用可能に。1年間のパブリックプレビューを経て正式版 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 6 | Tailwind CSS | v4.2.2 リリース | 新カラーパレット4種（mauve, olive, mist, taupe）、webpack プラグイン公式提供、論理プロパティユーティリティ追加 | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases) |
| 7 | Astro | v6 Beta | Vite Environment API ベースの開発サーバー刷新、Cloudflare Workers（workerd）ネイティブ統合、ライブコンテンツコレクション安定化 | [公式ブログ](https://astro.build/blog/astro-6-beta/) |
| 8 | Node.js | セキュリティリリース（v24.x / v22.x / v20.x） | 2026年3月24日に複数リリースラインのセキュリティ修正を一斉公開 | [Node.js Blog](https://nodejs.org/en/blog/vulnerability/march-2026-security-releases) |
| 9 | TypeScript | v7.0 (Project Corsa) 進行中 | Go で書き直されたネイティブコンパイラ `tsgo` により最大10倍の高速化。strict モードがデフォルト有効に | [InfoQ](https://www.infoq.com/news/2026/01/typescript-7-progress/) |
| 10 | Redis Enterprise for Kubernetes | v8.0.16-25 リリース | OSS Cluster API の外部クライアントサポート、ARM アーキテクチャ対応 | [Redis Docs](https://redis.io/docs/latest/operate/kubernetes/release-notes/8-0-16-releases/8-0-16-25-march2026/) |

## Deep Dive

- [Vite 8 — Rolldown 統合によるアーキテクチャ刷新](./tu-vite-8-rolldown.md)
