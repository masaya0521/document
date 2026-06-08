# Tech Updates — 2026-06-09

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | PostgreSQL | 19 Beta 1 リリース | 並列オートバキューム、FK 制約時のインサート最大2倍高速化、SQL/PGQ プロパティグラフ、`UPDATE/DELETE ... FOR PORTION OF`、`GROUP BY ALL`。JIT デフォルト無効化など破壊的変更あり | [News](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/) |
| 2 | PostgreSQL | 18.4 / 17.10 / 16.14 / 15.18 / 14.23 | 全サポート版の定例パッチ。11件のセキュリティ脆弱性と60件超のバグを修正 | [News](https://www.postgresql.org/about/news/postgresql-184-1710-1614-1518-and-1423-released-3297/) |
| 3 | Rust | 1.96.0 リリース | RFC3550 の新レンジ型（`core::range::Range` 等）安定化、`assert_matches!` マクロ追加、Wasm リンク時の未定義シンボル禁止。CVE-2026-5222/5223 修正 | [Blog](https://blog.rust-lang.org/2026/05/28/Rust-1.96.0/) |
| 4 | Python | 3.15 フィーチャーフリーズ / 3.15.0b2 | 6/2 に 3.15.0b2 公開、6月にフィーチャーフリーズ入り。3.14.5 は 5/10 リリース（pip 26.1 同梱、CVE-2026-3219 修正） | [Real Python](https://realpython.com/python-news-june-2026/) |
| 5 | SvelteKit | 2.61.0 リリース | `.run()` を廃止し `await query()` に統一（破壊的変更）、`query.live()` で長時間サブスクリプション対応、enhance 関数の改善 | [Blog](https://svelte.dev/blog/whats-new-in-svelte-june-2026) |
| 6 | Angular | 21.2.16 / 22 RC | 6/3 に 21.2.16 パッチ。Angular 22 が RC 段階（rc.1 は 5/20）で6月末〜の正式リリース見込み。Zoneless 変更検知・Vitest 統合が本番対応済み | [Events](https://angular.dev/events/v21) |
| 7 | Bun | v1.3.14 リリース | `Bun.Image`（ネイティブ依存なしの画像処理、メタ取得が sharp 比70倍）、`--linker=isolated` でウォームインストール約7倍、`Bun.serve()` の HTTP/3(QUIC) 実験対応 | [Blog](https://bun.com/blog/bun-v1.3.14) |
| 8 | Docker Desktop | 29.5.3 リリース | 6/4 公開。Docker Model Runner のレジストリミラー対応、`docker sbom` を `docker scout sbom` に置換、ネットワーク・Windows インストーラ修正 | [Release Notes](https://docs.docker.com/desktop/release-notes/) |
| 9 | Redis Insight | 3.4.1 GA | 専用の Search ワークスペースを追加。サンプル/既存データからのインデックス作成、補助エディタでのクエリ、Query Library への保存に対応 | [Docs](https://redis.io/docs/latest/) |
| 10 | Kubernetes | v1.37 マイルストーン | 6/9-10 に Production Readiness Freeze、6/16-17 に Enhancements Freeze。次期メジャーへ向けた機能確定フェーズ。1.33 は 6/28 に EOL | [Release Info](https://www.kubernetes.dev/resources/release/) |

## Deep Dive

- [PostgreSQL 19 Beta 1 — 並列オートバキュームと SQL/PGQ、破壊的変更](./tu-postgresql-19-beta1.md)
- [Rust 1.96.0 — 新レンジ型の安定化と assert_matches!](./tu-rust-1-96.md)
