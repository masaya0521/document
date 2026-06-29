# Tech Updates — 2026-06-30

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Deno | v2.9 リリース（6/25） | `deno desktop` で Web 技術からネイティブデスクトップアプリを構築。npm/pnpm/yarn/Bun からの第一級マイグレーション、CSS モジュールインポート、Node.js 26 互換に対応 | [Deno Blog](https://deno.com/blog) |
| 2 | Visual Studio Code | v1.126 リリース（6/24） | チャットセッション全体のコスト可視化、コンテキストサイズと推論努力度を統合した単一ピッカー、新規フォルダのデフォルト Restricted Mode 化（信頼バナー表示） | [Release Notes](https://code.visualstudio.com/updates/v1_126) |
| 3 | Vue.js | v3.6 リリース（6/11） | Vapor Mode の安定化が中心。Virtual DOM のオーバーヘッドを排除する新コンパイル戦略でランタイム性能とバンドルサイズを改善 | [VersionLog](https://versionlog.com/vuejs/3.6/) |
| 4 | Angular | v22.0.2 リリース（6/17） | Angular 22 系の最新安定版。Angular 21（2025/11）に続くメジャー更新 | [VersionLog](https://versionlog.com/angular/) |
| 5 | SvelteKit | v2.61.0 リリース（6 月） | Remote query を event handler / module scope で直接 await 可能に（共有キャッシュで dedupe）。`.run()` 廃止・enhance コールバックの引数変更など破壊的変更を含む | [What's new in Svelte](https://svelte.dev/blog/whats-new-in-svelte-june-2026) |
| 6 | Next.js | v16.2.7 安定版（6 月） | Turbopack / コンパイラ改善とバグ修正中心。React Server Components のキャッシュポイズニング等の脆弱性を修正するセキュリティフィックスを含む | [Releasebot](https://releasebot.io/updates/vercel/next-js) |
| 7 | Visual Studio 2026 | 6 月アップデート（6/23） | 「新時代」の VS。AI のプラットフォーム統合、性能改善に加え、Fluent カラートークンをテーマ単位で IDE 上から直接カスタマイズできる Theme colors ページを追加 | [Release Notes](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 8 | .NET / .NET Framework | 6 月サービシング更新（6/9） | セキュリティ・非セキュリティ修正を含む定例サービシングリリース | [.NET Blog](https://devblogs.microsoft.com/dotnet/dotnet-and-dotnet-framework-june-2026-servicing-updates/) |
| 9 | Terraform Kubernetes Provider | v3.2.0 リリース（6/4） | HashiCorp 公式 Kubernetes プロバイダの最新版。Terraform 本体も `init` クラッシュ修正や Linux s390x（zLinux）ビルド追加などを実施 | [Terraform Registry](https://registry.terraform.io/providers/hashicorp/kubernetes/latest) |
| 10 | Ruby / Sinatra | Ruby 3.4.4・Sinatra 4.0.1 | Ruby 3.4 系の保守リリースと、Sinatra 4.0.1 のメンテナンスリリース。RubyGems 3.6.x・Bundler 2.6.x も併せて更新 | [Ruby Releases](https://www.ruby-lang.org/en/downloads/releases/) |

## Deep Dive

- [Deno 2.9 — deno desktop と Node.js 26 互換](./tu-deno-2-9.md)
- [Vue 3.6 — Vapor Mode の安定化](./tu-vue-3-6.md)
