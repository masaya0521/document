# Tech Updates — 2026-06-08

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Node.js | リリーススケジュール変更（v27〜） | 年2回→年1回のメジャーリリースへ。全リリースを LTS 化し奇数/偶数の区別を廃止。v26 が現行モデル最後で、v27（2026年10月）から新方式に移行 | [InfoQ](https://www.infoq.com/news/2026/06/nodejs-release-changes/), [Node.js Blog](https://nodejs.org/en/blog/announcements/evolving-the-nodejs-release-schedule) |
| 2 | Node.js | v26.3.0 リリース（6/1） | Current ライン。Temporal API デフォルト有効、V8 14.6・Undici 8.0 などを取り込み。同日に Node.js 25 が EOL | [Node.js Releases](https://nodejs.org/en/about/previous-releases) |
| 3 | Angular | v22 リリース（6/3） | Resource API・Signal Forms が安定化。OnPush をデフォルト変更検知に、HttpClient が Fetch ベースに。`@Service` デコレータ追加、TypeScript 6 必須 | [Angular](https://angular.dev/events/v22), [Ninja Squad](https://blog.ninja-squad.com/2026/06/03/what-is-new-angular-22.0) |
| 4 | PostgreSQL | 19 Beta 1 リリース（6/4） | SQL/PGQ プロパティグラフクエリ、`ON CONFLICT DO SELECT`、`REPACK`、並列 autovacuum、`COPY TO` の JSON 出力。GA は 2026年秋予定 | [PostgreSQL](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/) |
| 5 | PostgreSQL | 18.4 等マイナーリリース | 18.4 / 17.10 / 16.14 / 15.18 / 14.23 を同時公開。11 件のセキュリティ脆弱性と 60 件超のバグを修正 | [PostgreSQL](https://www.postgresql.org/about/news/postgresql-184-1710-1614-1518-and-1423-released-3297/) |
| 6 | Deno | v2.9.0 リリース（6/3） | 直近メジャーの 2.6 では `dx`（npx 相当）、tsgo による高速型チェック、`deno audit`、source phase imports、より細かい権限制御を導入 | [Deno Releases](https://github.com/denoland/deno/releases), [Deno 2.6 Blog](https://deno.com/blog/v2.6) |
| 7 | Astro | v6.4.4 リリース | Rust 製 Markdown プロセッサ "Sätteri" を導入し、大規模ドキュメントサイトのビルドを 1 分以上短縮。Astro 自身の docs サイトでも効果を確認 | [Astro](https://docs.astro.build/en/guides/upgrade-to/v6/) |
| 8 | Next.js | v16.2.7 リリース | セキュリティ・バグ修正のバックポート。CVE-2026-23869 の修正サマリを公開 | [Vercel Changelog](https://vercel.com/changelog/summary-of-cve-2026-23869) |
| 9 | Go | go1.26.4 リリース（6/2） | Go 1.26 系のパッチリリース。1.25 系は今年初めにリリース済みで、現行メジャーは 1.26 | [Go Release History](https://go.dev/doc/devel/release) |
| 10 | VS Code | v1.123 リリース（6/3） | エージェント向け機能の強化、より大きなモデルコンテキスト対応、統合ブラウザの更新、一部拡張機能の自動更新遅延を追加 | [Visual Studio Magazine](https://visualstudiomagazine.com/) |

## Deep Dive

- [Angular 22 — Signal 安定化と OnPush デフォルト化](./tu-angular-22.md)
- [Node.js — 年1回メジャーリリースへの移行](./tu-nodejs-release-schedule.md)
