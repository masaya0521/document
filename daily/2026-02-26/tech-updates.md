# Tech Updates — 2026-02-26

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 Beta リリース | JS ベースコンパイラの最終メジャーバージョン。strict モードのデフォルト化、Temporal API 対応、ES5 ターゲット非推奨化。Go ベースの TS 7 への移行準備 | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/) |
| 2 | Go | 1.26 リリース | Green Tea GC がデフォルト化、実験的 SIMD パッケージ追加、`go fix` の全面書き直し、cgo オーバーヘッド約 30% 削減 | [Go Blog](https://go.dev/blog/go1.26) |
| 3 | PostgreSQL | 18.3, 17.9, 16.13, 15.17, 14.22 (臨時リリース) | 2/12 リリースで発生したリグレッション（`substring()` の非 ASCII テキストエラー、スタンバイサーバー停止）の修正 | [PostgreSQL News](https://www.postgresql.org/about/news/out-of-cycle-release-scheduled-for-february-26-2026-3241/) |
| 4 | VS Code | 1.109 (January 2026) | マルチエージェント開発プラットフォームへの進化。Claude Agent 統合、MCP Apps、エージェントセッション管理、ターミナルサンドボックス | [VS Code Updates](https://code.visualstudio.com/updates/v1_109) |
| 5 | FastAPI | 0.133.0 リリース | Pydantic + Rust による JSON レスポンスシリアライゼーションで 2 倍以上の性能向上。strict Content-Type チェックのデフォルト化 | [GitHub Releases](https://github.com/fastapi/fastapi/releases) |
| 6 | Svelte | 5.47 - 5.49 アップデート | カスタム `<select>` 要素の CSS サポート、CSS パーサー (`parseCss`) のエクスポート、カスタム要素の Shadow DOM 改善 | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-february-2026) |
| 7 | Rust | 1.93.1 ポイントリリース | 1.93.0 のバグ修正リリース。ソート実装の driftsort / ipnsort への置き換え、`build.build-dir` の安定化は 1.93.0 で導入済み | [Rust Blog](https://blog.rust-lang.org/2026/02/12/Rust-1.93.1/) |
| 8 | JetBrains IDE | 2025.3.3 アップデート | IntelliJ IDEA, WebStorm, PyCharm, GoLand 等の全 IDE で MCP サーバー出力スキーマ修正、プロキシ認証問題の解決 | [JetBrains Blog](https://blog.jetbrains.com/idea/2026/02/intellij-idea-2025-3-3/) |
| 9 | Redis Enterprise for K8s | 8.0.10-21 リリース | Redis Software 8.0.10-64 対応。OSS Cluster API の外部クライアントサポート、ARM アーキテクチャサポート追加 | [Redis Docs](https://redis.io/docs/latest/operate/kubernetes/release-notes/8-0-10-releases/8-0-10-21-feb2026/) |
| 10 | Visual Studio 2026 | February 2026 アップデート | Profiler Agent によるパフォーマンス分析の自動化、AI アシスタンス・診断機能の強化 | [Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |

## Deep Dive

- [TypeScript 6.0 Beta — Go ベースコンパイラへの移行準備](./tu-typescript-6-beta.md)
- [Go 1.26 — Green Tea GC と SIMD サポート](./tu-go-1-26.md)
