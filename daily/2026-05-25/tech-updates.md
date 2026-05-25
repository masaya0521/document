# Tech Updates — 2026-05-25

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | PostgreSQL | 18.0 リリース | 非同期 I/O サブシステム（最大3倍高速化）、virtual generated columns、uuidv7()、OAuth 認証サポート | [公式](https://www.postgresql.org/about/news/postgresql-18-released-3142/) |
| 2 | VS Code | 1.121 リリース | リモートエージェントセッション（SSH/dev tunnel 経由）、Mermaid・HTML プレビュー組み込み、Agent Host Protocol (AHP) | [公式](https://code.visualstudio.com/updates/v1_121) |
| 3 | Next.js | セキュリティリリース (15.5.18 / 16.2.6) | 13件の CVE を一括修正。DoS、SSRF、認証バイパス、キャッシュポイズニング、XSS 等。セルフホスト環境は即時アップデート推奨 | [Vercel](https://vercel.com/changelog/next-js-may-2026-security-release) |
| 4 | pnpm | 11.0 / 11.1 リリース | 11.0: SQLite ベースのストアインデックス、ESM 化、セキュリティデフォルト強化。11.1: `audit signatures` コマンド、GitHub Packages レジストリ対応 | [公式](https://pnpm.io/blog/releases/11.0) |
| 5 | Kotlin | VS Code 拡張機能 Alpha | JetBrains が KotlinConf 2026 で発表。IntelliJ の Kotlin プラグイン基盤を使った公式 Language Server | [JetBrains](https://blog.jetbrains.com/kotlin/2026/05/official-kotlin-support-for-visual-studio-code-is-now-available-in-alpha/) |
| 6 | Astro | 6.3 リリース | experimental advanced routing 導入。リクエストパイプラインの完全制御、Hono 等の外部フレームワーク統合が可能に | [公式](https://astro.build/blog/astro-630/) |
| 7 | Vercel AI SDK | Speech / Transcription サポート | `generateSpeech`・`transcribe` 関数を追加。OpenAI、ElevenLabs、Deepgram、Google 等のプロバイダに対応 | [Releasebot](https://releasebot.io/updates/vercel/vercel-ai) |
| 8 | JetBrains Rider | 2026.2 EAP 3 | AI エージェントによるテスト生成スキル（トークン消費50%削減）、intention preview、Godot テンプレート対応 | [JetBrains](https://blog.jetbrains.com/dotnet/2026/05/22/rider-2026-2-eap-3-cost-effective-agentic-test-coverage-code-change-previews-gamedev-templates-and-nuget-improvements/) |
| 9 | Visual Studio | 2026 May Update | Fluent カラートークンのカスタマイズ機能、C++ .vcxproj の NuGet PackageReference サポート（実験的） | [Microsoft](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 10 | Cloudflare R2 SQL | マルチテーブルクエリ対応 | Apache Iceberg テーブル間の JOIN、サブクエリ、self-join、マルチウェイ CTE をサポート | [Cloudflare](https://developers.cloudflare.com/changelog/post/2026-05-06-react-nextjs-vulnerabilities/) |

## Deep Dive

- [PostgreSQL 18 — 非同期 I/O と開発者向け新機能](./tu-postgresql-18.md)
- [VS Code 1.121 — リモートエージェントと Agent Host Protocol](./tu-vscode-1-121.md)
