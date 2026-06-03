# Tech Updates — 2026-06-04

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 7.0 Beta（Go 製ネイティブコンパイラ） | コンパイラを Go で書き直した Project Corsa が公開ベータに。`tsc` 比で約 10 倍高速（VS Code の 150 万行が 78 秒 → 7.5 秒）。RC は 6 月後半〜7 月初旬の見込み | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/) |
| 2 | Svelte / SvelteKit | June 2026 アップデート（SvelteKit 2.61.0 ほか） | remote query をイベントハンドラ・async コールバック・モジュールスコープで `await` 可能に。`query.live(...)` で長期サブスクリプション対応。`.run()` 廃止など破壊的変更あり | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-june-2026) |
| 3 | Next.js | 16.2 系 最新パッチ（6 月初旬） | dev モードで HTTP キャッシュ配信時の hydration 失敗を修正するなどバグフィックスを backport。メジャーは 3/18 リリースの 16.2（`next dev` 起動が約 400% 高速化） | [Next.js Blog](https://nextjs.org/blog/next-16-2) |
| 4 | Angular | 22.0.0-rc.1（5/20） | 「Signal-First」時代の本命リリース。selectorless components、Signal Forms の安定化、新規コンポーネントの OnPush デフォルト化、TypeScript 5.9 対応 | [Angular v22 Guide](https://www.herodevs.com/blog-posts/angular-version-history-every-release-date-support-window-and-end-of-life-date-from-angularjs-to-angular-22) |
| 5 | Vite | 8.0.16（6 月初旬） | Vite 8 系の最新パッチ。Rust 製バンドラ Rolldown を同梱し、Oxc ベースのツールチェーンへ移行が進む | [Vite Releases](https://vite.dev/releases) |
| 6 | PostgreSQL | 18.4 / 17.10 / 16.14 / 15.18 / 14.23（5/14） | 11 件のセキュリティ脆弱性と 60 件超のバグを修正。PostgreSQL 18 は新 I/O サブシステムでストレージ読み取り最大 3 倍高速化 | [PostgreSQL News](https://www.postgresql.org/about/news/postgresql-184-1710-1614-1518-and-1423-released-3297/) |
| 7 | Python | 3.14.5（5/10） | 3.14 系の最新パッチ。3.14 では free-threaded モードが正式サポート（実験的扱いを解除）、tail-call interpreter ベースの改良 JIT を搭載 | [Python Versions](https://versionlog.com/python/3.14/) |
| 8 | Go | 1.25.10（5/7） | 1.25 系の定例パッチリリース。月次でセキュリティ・バグフィックスを継続提供 | [Go Release History](https://go.dev/doc/devel/release) |
| 9 | VS Code | 1.122（5/28） | 週次リリースを継続。エージェント体験の強化と BYOK の柔軟化、ブラウザのデバイスエミュレーション、air-gapped BYOK サポートを追加 | [VS Code v1.122](https://code.visualstudio.com/updates/v1_122) |
| 10 | Redis Insight | 3.4.1 GA | 専用 Search ワークスペース（インデックス作成・クエリ・Query Library）を追加。Redis 8.8 対応、Linux ARM64 リリース（AppImage/deb/rpm）を追加 | [Redis Docs](https://redis.io/docs/latest/) |

## Deep Dive

- [TypeScript 7.0 Beta — Go 製ネイティブコンパイラ（Project Corsa）](./tu-typescript-7-0-beta.md)
- [Angular 22 — Signal-First 時代の到来](./tu-angular-22.md)
