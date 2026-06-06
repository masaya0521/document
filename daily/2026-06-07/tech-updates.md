# Tech Updates — 2026-06-07

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Go | go1.26.4 / go1.25.11（6/2 リリース） | `crypto/x509`・`mime`・`net/textproto` のセキュリティ修正と、コンパイラ・ランタイム・`go fix`・`crypto/fips140` のバグ修正。両系列同日リリースで早めの更新推奨 | [Go Release History](https://go.dev/doc/devel/release) |
| 2 | Deno | v2.8.2（6/3 リリース） | 6/3 のパッチで compile・crypto・install・LSP を改善。先行する 2.8（5/22）では pnpm 互換の catalog プロトコルで monorepo のバージョン一元管理に対応 | [Deno v2.8.2](https://github.com/denoland/deno/releases/tag/v2.8.2), [Deno 2.8 Blog](https://deno.com/blog/v2.8) |
| 3 | VS Code | 1.123（6/3 リリース） | チャットセッションの GitHub アカウント同期、複数エージェントを並べる Agent ウィンドウ（プレビュー）、Research エージェント、Anthropic/OpenAI モデルの 1M コンテキスト対応 | [VS Code 1.123](https://code.visualstudio.com/updates/v1_123) |
| 4 | Terraform Kubernetes Provider | v3.2.0（6/4 リリース） | HashiCorp 公式 Kubernetes プロバイダのマイナーリリース。Terraform から K8s リソースを管理する最新版 | [Terraform Registry](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs) |
| 5 | pnpm | 11.5.2（6/5 リリース） | pnpm 11 系の最新パッチ。pnpm 11 はサプライチェーン対策として `minimumReleaseAge`（1日）をデフォルト有効化、Store v11（SQLite 化）、pure ESM 配布へ移行 | [pnpm Releases](https://github.com/pnpm/pnpm/releases), [pnpm 11.0](https://pnpm.io/blog/releases/11.0) |
| 6 | Next.js | 16.2 | Adapters 導入、`next dev` 起動が約 400% 高速化・レンダリング約 50% 高速化、Turbopack の Server Fast Refresh・SRI 対応、新 500 エラーページ、実験的 Agent DevTools。6月は backport 中心 | [Next.js 16.2](https://nextjs.org/blog/next-16-2) |
| 7 | SvelteKit / Svelte | 2026年6月ダイジェスト（SvelteKit 2.61.0 ほか） | リモート関数の `.run()` 廃止（`await query()` へ）、`query.live()` の async-iterable 化、enhance コールバック仕様変更、language-tools の TypeScript 6.0 対応 | [What's new in Svelte: June 2026](https://svelte.dev/blog/whats-new-in-svelte-june-2026) |
| 8 | Bun | v1.3.14 | 組み込み画像処理 API `Bun.Image`、`fetch()` の実験的 HTTP/2・HTTP/3 クライアントと `Bun.serve()` の HTTP/3(QUIC) 対応、isolated linker のグローバルストアで warm install 7倍高速化、`fs.watch()` 再実装 | [Bun Blog](https://bun.com/blog) |
| 9 | Astro | 6.4 | Rust 製 Markdown プロセッサ「Sätteri」を導入し Markdown 主体サイトのビルドを大幅高速化（公式 docs サイトで 1分以上短縮） | [Astro Blog](https://astro.build/blog/) |
| 10 | Tailwind CSS | v4.3 | Oxide エンジン世代の v4 系最新マイナー。ユーティリティ・設定面の改善を継続 | [Tailwind CSS Releases](https://github.com/tailwindlabs/tailwindcss/releases) |

## Deep Dive

- [Next.js 16.2 — Adapters とパフォーマンス刷新](./tu-nextjs-16-2.md)
- [pnpm 11 — サプライチェーン対策のデフォルト化と Store v11](./tu-pnpm-11.md)
