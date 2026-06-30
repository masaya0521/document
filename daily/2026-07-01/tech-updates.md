# Tech Updates — 2026-07-01

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 7.0 RC リリース | コンパイラを Go へ移植した「Project Corsa」が RC 到達。型チェック約10倍高速化・メモリ約50%削減。GA は RC から約1ヶ月以内を予定 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-rc/) |
| 2 | Deno | 2.9 リリース | `deno desktop` で Web スタックからネイティブデスクトップアプリを単一バイナリで生成。npm/pnpm/yarn/Bun のロックファイル直読みに対応 | [公式ブログ](https://deno.com/blog/v2.9) |
| 3 | Rust | 1.96.1 ポイントリリース | Cargo の HTTP クライアントのリトライ/タイムアウト欠落と MIR 最適化の誤コンパイルを修正。libssh2 の CVE 3件にも対応 | [Rust Blog](https://blog.rust-lang.org/2026/06/30/Rust-1.96.1/) |
| 4 | VS Code | 1.126 リリース | セッション単位のコストトラッキング、1セッション内での複数チャット並行実行、制限モードでの安全なワークスペース信頼ブラウジングを追加 | [リリースノート](https://code.visualstudio.com/updates/v1_126) |
| 5 | Go | 1.25.11 リリース | `crypto/x509`・`mime`・`net/textproto` のセキュリティ修正、コンパイラ・ランタイムのバグ修正を含むパッチリリース | [Release History](https://go.dev/doc/devel/release) |
| 6 | Python | 3.14.6 / 3.13.14 リリース | 3.14 系の最新安定版が 3.14.6 に。3.13.14 も 2026-06-10 にリリースされ、両系統でメンテナンスが継続 | [Status of Python versions](https://devguide.python.org/versions/) |
| 7 | Vite | 8.0 リリース | デュアルバンドラ構成から Rust 製の統合バンドラ Rolldown へ全面移行。ビルドが最大30倍高速化（46秒→6秒の事例も） | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 8 | Django | 6.0.6 リリース | Django 6.0 系の最新メンテナンスリリース。6.0 はサポート期限 2027-04-30 まで | [リリースノート](https://docs.djangoproject.com/en/6.0/releases/) |
| 9 | Bun | 1.3.x 系継続更新 | 1.3 で導入されたゼロコンフィグなフロントエンド配信・ネイティブ MySQL/Redis クライアントに加え、1.3.14 までパッチが継続 | [Changelog](https://www.changes.watch/products/bun) |
| 10 | PostgreSQL | 18.4 リリース | 18 系の最新マイナー。セキュリティ脆弱性11件・バグ60件超を修正。18 本体は非同期 I/O サブシステムやデータチェックサムのデフォルト有効化が目玉 | [リリース告知](https://www.postgresql.org/about/news/postgresql-184-1710-1614-1518-and-1423-released-3297/) |

## Deep Dive

- [TypeScript 7.0 RC — Go ネイティブコンパイラ](./tu-typescript-7-0-rc.md)
- [Deno 2.9 — deno desktop](./tu-deno-2-9.md)
