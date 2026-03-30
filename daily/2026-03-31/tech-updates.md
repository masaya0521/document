# Tech Updates — 2026-03-31

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 リリース | JavaScript ベース最後のメジャーバージョン。`strict: true` がデフォルト化、Temporal API 対応、多数の非推奨化により Go ネイティブの 7.0 への移行を準備 | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 2 | Vite | 8.0 リリース | Rolldown（Rust 製統一バンドラー）を搭載し、ビルド速度 10-30x 向上。Linear は 46秒→6秒に改善。Vite Devtools 統合、プラグインレジストリ公開 | [Vite Blog](https://vite.dev/blog/announcing-vite8) |
| 3 | JetBrains IDE | 2026.1 一斉リリース | IntelliJ IDEA・WebStorm・GoLand・Rider・CLion が 2026.1 をリリース。AI エージェント統合強化、ネイティブ Wayland 対応、WebStorm は TypeScript 6 対応 | [IntelliJ Blog](https://blog.jetbrains.com/idea/2026/03/intellij-idea-2026-1/) |
| 4 | ReSharper | VS Code 対応 & 2026.1 | ReSharper の C# ツーリングが VS Code・Cursor 等でも利用可能に。パフォーマンスモニタリングツールウィンドウも新搭載 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/30/resharper-2026-1-released/) |
| 5 | GitHub Copilot | コーディングエージェント改善 | エージェントセッションの可視性向上、Actions ワークフロー承認スキップ設定追加、コードレビューのエージェントアーキテクチャ移行 | [GitHub Changelog](https://github.blog/changelog/2026-03-19-more-visibility-into-copilot-coding-agent-sessions/) |
| 6 | Tailwind CSS | @tailwindcss/vite 4.2.2 | Vite 8 対応（peer dependency に ^8.0.0 追加）。Tailwind CSS の Vite プラグインが最新エコシステムに追従 | [GitHub PR](https://github.com/tailwindlabs/tailwindcss/pull/19790) |
| 7 | Deno | 2.7.1 リリース | 安定版の継続的なリリース。npm 互換性の成熟、dx コマンド（npx 相当）の安定化が進行中 | [GitHub Releases](https://github.com/denoland/deno/releases) |
| 8 | GoLand | 2026.1 — Go 1.26 対応 | Go 1.26 のシンタックス更新のガイド付き適用、Git worktree サポート、AI エージェント拡張 | [GoLand Blog](https://blog.jetbrains.com/go/2026/03/26/goland-2026-1-is-released/) |
| 9 | Visual Studio | 2026 (17.14) 3月アップデート | JSON エディタのコアエディタ統合、Copilot Agent Skills の自動検出、HTML クリップボード対応 | [VS Release Notes](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 10 | Redis Enterprise | K8s 7.8.6-13 | Kubernetes 向けメンテナンスリリース。Redis Software 7.8.6-256 のサポートを追加 | [GitHub Releases](https://github.com/RedisLabs/redis-enterprise-k8s-docs/releases) |

## Deep Dive

- [TypeScript 6.0 — JavaScript ベース最後のメジャーリリースと 7.0 移行ガイド](./tu-typescript-6-0.md)
- [Vite 8.0 — Rolldown 統合による統一バンドラーアーキテクチャ](./tu-vite-8-0.md)
