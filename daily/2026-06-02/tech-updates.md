# Tech Updates — 2026-06-02

直近（主に 2026年5月）にリリース・公開された、開発者が日常的に使う技術のアップデート情報を10件厳選しました。ランタイム・フレームワーク・言語・開発ツールの動きが中心です。

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Node.js | v26.0.0 / v26.2.0 リリース | Temporal API がフラグなしでデフォルト有効化。V8 14.6、Undici 8 同梱。レガシー `_stream_*` モジュール等を削除 | [Release v26.0.0](https://github.com/nodejs/node/releases/tag/v26.0.0) / [v26.2.0](https://github.com/nodejs/node/releases/tag/v26.2.0) |
| 2 | Bun | v1.3.14 リリース | 組み込み画像処理 API `Bun.Image`（Sharp 代替）、fetch の実験的 HTTP/2・HTTP/3、`Bun.serve()` の HTTP/3(QUIC)、isolated linker で warm install が 7倍高速化 | [Bun v1.3.14 Blog](https://bun.com/blog/bun-v1.3.14) |
| 3 | Deno | v2.8.0 リリース（5/27） | `deno audit fix` の追加、新しい CI ワークフロー、npm パッケージング対応。2.7 で安定化した Temporal を踏襲 | [Deno Releases](https://github.com/denoland/deno/releases) |
| 4 | Angular | v22 リリース（5/16 頃） | Signal Forms・Signals API・Zoneless が安定化。変更検知のデフォルトが OnPush に。`httpResource`/`rxResource` も stable | [Announcing Angular v21/v22](https://blog.angular.dev/announcing-angular-v21-57946c34f14b) |
| 5 | Python | 3.15.0b1 リリース（5/11、機能凍結） | 遅延インポート、ゼロオーバーヘッドのサンプリングプロファイラ、free-threaded 向け安定 ABI、デフォルト UTF-8 化が進行。3.14.5 も 5/10 リリース | [Python 3.15 What's New](https://docs.python.org/3.15/whatsnew/3.15.html) |
| 6 | VS Code | v1.122 リリース（5/28） | 互換モデルで 1M トークンコンテキスト対応、エージェント専用ウィンドウ（プレビュー）、GitHub サインイン不要の air-gapped BYOK、ブラウザのデバイスエミュレーション | [VS Code 1.122](https://code.visualstudio.com/updates/v1_122) |
| 7 | CodeQL | v2.25.5 リリース（5/28） | GitHub Actions 上でのクエリ精度を改善。Code Scanning の検出品質向上 | [GitHub Changelog](https://github.blog/changelog/) |
| 8 | npm (GitHub) | 段階公開（phased publishing）（5/22） | パッケージの段階的ロールアウトと、インストール時の新しい制御オプションを追加 | [GitHub Changelog](https://github.blog/changelog/) |
| 9 | Tailwind CSS | v4.3 系 | `@tailwindcss/vite` プラグイン経由のセットアップが標準化。`@theme` による CSS-first 設計トークン定義 | [Tailwind CSS Docs](https://tailwindcss.com/docs/installation/framework-guides/astro) |
| 10 | Vite / VoidZero | Vite 8 beta・Oxfmt beta | Vite 8 beta で実験的 devtools とプラグインレジストリ（registry.vite.dev）。Oxfmt beta は Prettier の JS/TS 適合テスト 100% 通過・最大36倍高速 | [What's New in ViteLand](https://voidzero.dev/posts/whats-new-feb-2026) |

## Deep Dive

- [Node.js 26 — Temporal API デフォルト有効化](./tu-node-26.md)
- [Bun v1.3.14 — Bun.Image と HTTP/3 対応](./tu-bun-1-3-14.md)
