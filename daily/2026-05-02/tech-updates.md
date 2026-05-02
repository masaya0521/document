# Tech Updates — 2026-05-02

直近2週間で開発者インパクトが大きかったソフトウェア技術アップデート 10 件を厳選。

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Node.js | v26.0.0（2026-04-28） | Temporal API がデフォルト有効化、V8 14.6 / Undici 8.0 へ更新。10月に LTS 入り予定の Current ライン。 | [GitHub PR](https://github.com/nodejs/node/pull/62526) |
| 2 | pnpm | v11.0（2026-04-28） | ESM 化、JSON-per-package ストアを SQLite 1 ファイル化、`minimumReleaseAge=1440` などサプライチェーン防御をデフォルト ON。Node.js 22+ 必須。 | [pnpm Blog](https://pnpm.io/blog/releases/11.0) |
| 3 | Visual Studio Code | v1.118（2026-04-29） | Copilot CLI のリモート操作、ワークスペース横断のセマンティック検索、トークン効率改善（6/1 の Copilot 従量課金移行を見据えた最適化）。 | [VS Code Updates](https://code.visualstudio.com/updates/v1_118) |
| 4 | GitHub Copilot CLI | v1.0.40（2026-05-01） | MCP サーバー向け `client_credentials` OAuth grant に対応しヘッドレス認証可能に。`/clear` `/new` でカスタムエージェントもリセット。 | [Releases](https://github.com/github/copilot-cli/releases) |
| 5 | Rust | v1.95.0（2026-04-16） | `cfg_select!` マクロ追加（`cfg-if` クレート相当の機能を標準化）、`match` 腕での if-let guard 安定化、PowerPC のインラインアセンブリ安定化。 | [Rust Blog](https://blog.rust-lang.org/2026/04/16/Rust-1.95.0/) |
| 6 | Next.js | v16.2（2026-03-18、最新パッチ 16.2.4 が 2026-04-16） | `next dev` 起動 ~400% 高速化、レンダリング ~50% 高速化、Adapter API 安定化、新500ページデザイン。 | [Next.js Blog](https://nextjs.org/blog) |
| 7 | Astro | v6.2（2026-04） | 実験的 JSON ロガー（コーディングエージェント向け構造化ログ）、`svgOptimizer` API 再設計、`experimental_getFontFileURL()` で OG 画像生成支援。 | [Astro Blog](https://astro.build/blog/astro-620/) |
| 8 | Python | 3.14.4 / 3.15.0a8（2026-04-07） | 3.14 系の保守リリースと 3.15 アルファ。3.14.5 と 3.15.0b1 がそれぞれ 2026-05-08 / 2026-05-05 に予定されている。 | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/) |
| 9 | Go | v1.26.2（2026-04-07） | 1.26 系初の重要パッチ（セキュリティ・バグ修正）。1.26 本体は 2026-02-10 リリースで Green Tea GC がデフォルト化、`crypto/hpke` 等の新パッケージ追加。 | [Go Release Notes](https://go.dev/doc/devel/release) |
| 10 | Bun | v1.3.13（2026-04 中旬） | テストランナー機能拡張を含むパッチ。Anthropic 買収後のメモリリーク修正系も継続的に取り込み中。2.0 はロードマップ上 2026 年後半。 | [Bun Blog](https://bun.com/blog/bun-v1.3.13) |

## Deep Dive

- [Node.js 26 — Temporal がついにデフォルト有効化](./tu-node-26.md)
- [pnpm 11 — サプライチェーン防御デフォルト ON と SQLite ストア](./tu-pnpm-11.md)
