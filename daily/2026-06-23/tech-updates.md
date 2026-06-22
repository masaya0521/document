# Tech Updates — 2026-06-23

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Go | v1.27 RC1 リリース | ジェネリックメソッド対応、`encoding/json/v2`、`crypto/mldsa`（ML-DSA）、小サイズアロケーション最適化など。正式版は8月予定 | [golang-announce](https://groups.google.com/g/golang-announce/c/Cu9HkstbtpA/m/NfBgswyTBgAJ), [Release Notes](https://go.dev/doc/go1.27) |
| 2 | Python | v3.13.14 リリース | 3.13 系の14回目のメンテナンスリリース。約240件のバグ修正・ビルド改善・ドキュメント更新（6/10） | [Python.org](https://www.python.org/downloads/release/python-31314/) |
| 3 | Go | v1.26.4 / v1.25.11 セキュリティリリース | `crypto/x509`・`mime`・`net/textproto` のセキュリティ修正、コンパイラ／ランタイムのバグ修正（6/2） | [Release History](https://go.dev/doc/devel/release) |
| 4 | SvelteKit | v2.61.0 リリース | `.run()` 削除（破壊的変更）、イベントハンドラ等での `await query()` 対応、`query.live()` の非同期イテラブル化 | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-june-2026) |
| 5 | Svelte | v5.56.0 リリース | テンプレートのマークアップ内で宣言を直接記述可能に | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-june-2026) |
| 6 | Vite | v8.0 リリース | Rolldown をデフォルトバンドラに統合。Vue/Nuxt/Svelte/Solid/Astro 等の標準ビルドツールとして定着 | [Vite Blog](https://vite.dev/blog/announcing-vite8) |
| 7 | Redis | v8.8 / Redis Insight 3.4.1 | Redis 8.8 でクライアントライブラリ・CI 対応を拡充。Redis Insight 3.4.1 が GA | [releases.sh](https://releases.sh/redis/releases) |
| 8 | Tailwind CSS | v4.3.1 リリース | v4 系のメンテナンスリリース（6月中旬） | [npm](https://www.npmjs.com/package/tailwindcss) |
| 9 | Astro | v6.4.4 リリース | 6 系の最新パッチ。ゼロ JS デフォルトのコンテンツ志向フレームワークとして安定運用 | [Astro Releases](https://github.com/withastro/astro/releases) |
| 10 | Next.js | v16.2.7 リリース | 16 系の最新パッチリリース | [Next.js Releases](https://github.com/vercel/next.js/releases) |

## Deep Dive

- [Go 1.27 RC1 — ジェネリックメソッドと encoding/json/v2](./tu-go-1-27-rc1.md)
