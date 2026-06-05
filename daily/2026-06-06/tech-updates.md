# Tech Updates — 2026-06-06

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Go | go1.26.4 リリース（6/2） | `crypto/x509`・`mime`・`net/textproto` のセキュリティ修正と、コンパイラ／ランタイム／`crypto/fips140`・`go fix` のバグ修正を含む安定版パッチ | [Release History](https://go.dev/doc/devel/release) |
| 2 | Python | 3.15.0b2 リリース（6/2） | 次期メジャー 3.15 のベータ第2弾。安定版（3.14系）と並行して新機能の検証が進行中 | [Status of Python versions](https://devguide.python.org/versions/) |
| 3 | VS Code | 1.123 リリース（6/3） | エージェント向け機能強化、より大きなモデルコンテキスト対応、内蔵ブラウザ更新、一部拡張機能の自動更新遅延を追加。webview は anchor positioning でレイアウト性能改善 | [Releasebot](https://releasebot.io/updates/microsoft/visual-studio-code) |
| 4 | Svelte / SvelteKit | June 2026 マンスリー（SvelteKit 2.61.0 ほか） | `query.run()` の削除、リモートクエリの非同期化（イベントハンドラ・async コールバック・モジュールスコープで `await` 可能）、`query.live(...)` の async-iterable 化。Svelte 5.56.0 でマークアップ内宣言が可能に | [What's new in Svelte](https://svelte.dev/blog/whats-new-in-svelte-june-2026) |
| 5 | Rust | 1.96.0 リリース（5/28） | `core::range` の新 Range 型（`Copy` 可能・`IntoIterator` 実装）、`assert_matches!`/`debug_assert_matches!` の安定化、WebAssembly の暗黙的 `--allow-undefined` 削除、Cargo 脆弱性2件（CVE-2026-5222/5223）の修正 | [Rust Blog](https://blog.rust-lang.org/2026/05/28/Rust-1.96.0/) |
| 6 | Redis | Redis Insight 3.4.1 GA / node-redis 6.0 / Redis 8.8 対応 | Redis Insight 3.4.1 が専用 Search ワークスペースと Linux ARM64 パッケージを追加。node-redis 6.0 は RESP3 をデフォルト化し最低 Node.js バージョンを引き上げ | [endoflife.date/redis](https://endoflife.date/redis) |
| 7 | Next.js | June 2026 セキュリティパッチ | RSC のキャッシュポイズニングや middleware/proxy リダイレクトに関する複数の advisory を修正。prerender recovery・route params・cache key 等のコア修正をバックポート | [Releasebot](https://releasebot.io/updates/vercel/next-js) |
| 8 | PostgreSQL | 18.4 ほか（5/14） | 18.4 / 17.10 / 16.14 / 15.18 / 14.23 のマイナーリリース。11件のセキュリティ脆弱性と60件超のバグを修正 | [PostgreSQL News](https://www.postgresql.org/about/news/postgresql-184-1710-1614-1518-and-1423-released-3297/) |
| 9 | pnpm | 11.0 リリース（4/28） | npm CLI フォールバックを廃止しネイティブ publish 実装へ、ストアを SQLite 単一 DB 化、グローバルインストールを分離。Node.js 22+ 必須・pnpm 自体が pure ESM 化 | [pnpm Blog](https://pnpm.io/blog/releases/11.0) |
| 10 | Bun | 1.3（フロントエンド開発強化） | `bun index.html` のゼロコンフィグなフロント配信・HMR、SQLite/Postgres に加えネイティブ MySQL クライアント追加、`bun.lock` テキストロックファイルをデフォルト化 | [Bun](https://bun.com/) |

## Deep Dive

- [Rust 1.96.0 — 新 Range 型・assert_matches! と WASM リンカ挙動変更](./tu-rust-1-96.md)
- [SvelteKit June 2026 — リモートクエリの非同期化と `query.run()` 削除](./tu-sveltekit-june-2026.md)
