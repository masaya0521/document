# Tech Updates — 2026-05-24

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Node.js | v26.0.0 リリース | Temporal API デフォルト有効化、V8 14.6、Undici 8、レガシー API の大規模削除 | [GitHub](https://github.com/nodejs/node/releases/tag/v26.0.0) |
| 2 | Bun | Zig→Rust リライトがマージ | 960K 行を AI（Claude Code）で 6 日間で Rust に移植。99.8% のテストをパス | [The Register](https://www.theregister.com/devops/2026/05/14/anthropics-bun-rust-rewrite-merged-at-speed-of-ai/5240381) |
| 3 | Next.js / React | セキュリティリリース（13 CVE） | DoS・ミドルウェアバイパス・SSRF・XSS 等 13 件の脆弱性を修正。15.5.18 / 16.2.6 へ即時アップグレード推奨 | [Vercel](https://vercel.com/changelog/next-js-may-2026-security-release) |
| 4 | Kubernetes | v1.36 "Haru" + パッチ 1.36.1 | 70 の新機能。User Namespaces・Mutating Admission Policies が GA 化。AI/ML ワークロード対応強化 | [Kubernetes Blog](https://kubernetes.io/blog/2026/04/22/kubernetes-v1-36-release/) |
| 5 | JetBrains Rider | 2026.2 EAP 3 | AI エージェントによるテスト生成のトークンコスト最適化、コード変更プレビュー、NuGet UI 刷新 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/05/22/rider-2026-2-eap-3-cost-effective-agentic-test-coverage-code-change-previews-gamedev-templates-and-nuget-improvements/) |
| 6 | PostgreSQL | 18.4 / 17.10 等リリース | 定期セキュリティ＆バグ修正リリース。18.x 系の 4 回目のパッチ | [PostgreSQL](https://www.postgresql.org/about/news/postgresql-183-179-1613-1517-and-1422-released-3246/) |
| 7 | Visual Studio | 2026 May Update | Copilot エージェントのスキル自動検出、テーマカラー直接カスタマイズ、PR 管理の統合 | [Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 8 | Deno | 2.7 リリース | Temporal API 安定化（フラグ不要に）、Windows ARM 公式ビルド、npm overrides 対応 | [Deno Blog](https://deno.com/blog/v2.7) |
| 9 | Rust | 1.95.0 リリース | `if let` ガードの安定化、`cfg_select!` マクロ追加、Power アーキテクチャ向けインラインアセンブリ安定化 | [Rust Blog](https://blog.rust-lang.org/releases/latest/) |
| 10 | Astro | 6.2 リリース | 構造化ログ対応のカスタムロガー（実験的）、SVG オプティマイザー API 刷新、v7 アルファプレビュー | [Astro Blog](https://astro.build/blog/astro-620/) |

## Deep Dive

- [Node.js 26.0.0 — Temporal API 時代の幕開け](./tu-nodejs-26.md)
- [Bun — 960K 行の Zig→Rust AI リライト](./tu-bun-rust-rewrite.md)
