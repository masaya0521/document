# Tech Updates — 2026-05-28

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Kotlin | VS Code Extension Alpha | KotlinConf 2026 で発表。IntelliJ のコードインサイト基盤を利用した公式 Kotlin Language Server による VS Code サポート | [JetBrains Blog](https://blog.jetbrains.com/kotlin/2026/05/official-kotlin-support-for-visual-studio-code-is-now-available-in-alpha/) |
| 2 | Rider | 2026.2 EAP 3 | AI エージェントによるテストカバレッジ生成、コード変更プレビュー、GameDev テンプレート追加 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/05/22/rider-2026-2-eap-3-cost-effective-agentic-test-coverage-code-change-previews-gamedev-templates-and-nuget-improvements/) |
| 3 | pnpm | 11.2 リリース | pacquet（Rust 実装）を実験的インストールバックエンドとして統合。`pnpm login --scope` 実装 | [pnpm Blog](https://pnpm.io/blog/releases/11.2) |
| 4 | PostgreSQL | 18.4 パッチリリース | セキュリティ修正およびバグ修正パッチ | [PostgreSQL](https://www.postgresql.org/docs/release/18.2/) |
| 5 | VS Code | 1.120 リリース | Agents ウィンドウが Stable に昇格。BYOK モデルのトークン使用量追跡、ターミナルコマンドリスク評価 | [VS Code](https://code.visualstudio.com/updates/v1_120) |
| 6 | Bun | 1.3.14 リリース | Bun.Image（画像処理 API）、HTTP/2・HTTP/3 クライアント、7x 高速 warm install、FreeBSD・Android ビルド対応 | [Bun Blog](https://bun.com/blog/bun-v1.3.14) |
| 7 | IntelliJ IDEA | 2026.2 EAP 開始 | MCP でデバッグセッション操作（ブレークポイント・ログポイント）、エージェントスキルリポジトリ、AI フルメソッド生成 | [JetBrains Blog](https://blog.jetbrains.com/idea/2026/05/intellij-idea-2026-2-eap/) |
| 8 | Go | 1.26.3 / 1.25.10 セキュリティ修正 | html/template, net/http, net/mail, syscall 等のセキュリティ修正 | [Go Release History](https://go.dev/doc/devel/release) |
| 9 | Next.js / React | セキュリティリリース | 13 CVE パッチ — DoS, SSRF, ミドルウェアバイパス, キャッシュポイズニング, XSS。15.5.18 / 16.2.6 へのアップグレード推奨 | [Vercel Changelog](https://vercel.com/changelog/next-js-may-2026-security-release) |
| 10 | pnpm | 11.0 メジャーリリース | SQLite ベースのストアインデックス、サプライチェーン保護デフォルト有効、ネイティブ publish 実装、Node.js 22+ 必須 | [pnpm Blog](https://pnpm.io/blog/releases/11.0) |

## Deep Dive

- [pnpm 11 — SQLite ストア・サプライチェーン保護・pacquet 統合](./tu-pnpm-11.md)
- [Kotlin VS Code Extension Alpha — KotlinConf 2026 ハイライト](./tu-kotlin-vscode-kotlinconf-2026.md)
