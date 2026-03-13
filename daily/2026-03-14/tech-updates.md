# Tech Updates — 2026-03-14

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 RC | JavaScript ベース最後のリリース。RegExp.escape、ES2025 サポート、--stableTypeOrdering フラグなど。TS 7.0（Go ベース）への橋渡し | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/) |
| 2 | Vite | 8.0 リリース | Rolldown を統一バンドラーとして採用し 10-30x 高速化。Module Federation、永続キャッシュ、統合 Devtools を搭載 | [Vite Blog](https://vite.dev/blog/announcing-vite8) |
| 3 | PostgreSQL | 18.3 / 17.9 等パッチリリース | PostgreSQL 18 系の最新パッチ。18 では非同期 I/O、uuidv7()、OAuth 2.0 認証、スキップスキャンなどが導入済み | [Clever Cloud](https://www.clever.cloud/developers/changelog/2026/03-09-pg-update-18.3) |
| 4 | Deno | 2.7.4 | コア互換性修正、Node.js アサーション互換、TTY stdout/stderr 処理改善、npm パッケージ起動パフォーマンス向上 | [GitHub Releases](https://github.com/denoland/deno/releases) |
| 5 | JetBrains ReSharper | VS Code / Cursor 対応版正式リリース | 1年間の Public Preview を経て正式版に。C# コード解析、リファクタリング、フォーマットを VS Code 系エディタで利用可能 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 6 | VS Code | 2026年2月版リリース | エージェント機能の大幅強化、バックグラウンドエージェント、Claude 統合、セッションメモリ、コンテキスト圧縮、フォークチャット機能 | [Releasebot](https://releasebot.io/updates/microsoft/visual-studio-code) |
| 7 | Tailwind CSS | v4.2.1 | Vite 8 対応を含むメンテナンスリリース | [npm](https://www.npmjs.com/package/@tailwindcss/vite) |
| 8 | JetBrains IDE | 2026.1 リリース準備中 | 3月24日の週にリリース予定。プラグイン互換性チェックが呼びかけられている | [JetBrains Platform](https://platform.jetbrains.com/t/2026-1-is-coming-time-to-check-your-plugin-compatibility/3865) |
| 9 | Go | 1.24.13 セキュリティパッチ | go コマンド、crypto/tls パッケージのセキュリティ修正（2月4日リリース、現行最新） | [Go Release History](https://go.dev/doc/devel/release) |
| 10 | Deno 2.7 | Temporal API 安定化 | Temporal API の安定化、Windows ARM ビルド、npm overrides、Brotli 圧縮ストリーム、自己解凍コンパイルバイナリ、deno create コマンド追加 | [Deno Blog](https://deno.com/blog) |

## Deep Dive

- [TypeScript 6.0 RC — Go ベースへの橋渡しリリース](./tu-typescript-6-0-rc.md)
- [Vite 8.0 — Rolldown 統合による次世代ビルドツール](./tu-vite-8.md)
