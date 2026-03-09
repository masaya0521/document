# Tech Updates — 2026-03-10

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 RC リリース | JS ベース最後のリリース。strict デフォルト化、module: esnext / target: es2025 へ変更、ES5 ターゲット廃止など大規模な破壊的変更。Go ベースの 7.0 への橋渡し | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/) |
| 2 | Rust | 1.94.0 リリース | array_windows メソッドの安定化、AVX-512 FP16 intrinsics のサポート、Cargo の include キーによるモジュラー設定、TOML 1.1 対応 | [Rust Blog](https://blog.rust-lang.org/releases/latest/) |
| 3 | Go | 1.26.1 パッチリリース | Go 1.26 のセキュリティ修正・バグ修正。1.26 本体は new(expr) 構文、crypto/hpke パッケージ、実験的 SIMD サポートなどを含む | [Go Release History](https://go.dev/doc/devel/release) |
| 4 | Deno | 2.7.4 リリース | Temporal API の安定化、Windows ARM 対応、npm overrides サポート、Brotli 圧縮ストリーム、自己展開コンパイルバイナリ | [Deno Blog](https://deno.com/blog/v2.7) |
| 5 | Vite | 8 Beta リリース | Rolldown（Rust ベースバンドラー）統合で本番ビルド 10-30x 高速化。esbuild + Rollup のデュアル構成を単一の Rust ソリューションに統一 | [Vite Blog](https://vite.dev/blog/announcing-vite8-beta) |
| 6 | Tailwind CSS | 4.2.0 リリース | webpack プラグイン追加、新カラーパレット4種（mauve, olive, mist, taupe）、論理プロパティユーティリティ、font-features ユーティリティ | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases) |
| 7 | VS Code | 1.110（February 2026）リリース | エージェント機能の大幅強化 — バックグラウンドエージェント制御、Claude 統合、セッションメモリ、コンテキスト圧縮、フォークチャット | [Releasebot](https://releasebot.io/updates/microsoft/visual-studio-code) |
| 8 | Astro | 6 Beta リリース | Vite Environment API ベースの新開発サーバー、Workerd 統合で Dev === Prod パリティ実現、ライブコンテンツコレクション、組み込み CSP サポート | [Astro Blog](https://astro.build/blog/astro-6-beta/) |
| 9 | PostgreSQL | 18.3 / 17.9 等リリース | 2/26 の定期リリースで導入されたリグレッションを修正するアウトオブサイクルリリース | [PostgreSQL News](https://www.postgresql.org/about/news/postgresql-181-177-1611-1515-1420-and-1323-released-3171/) |
| 10 | Python | 3.12.13 / 3.11.15 / 3.10.20 | 3/3 リリースのセキュリティバグ修正。3.14 は 2025/10 に GA 済み（テンプレート文字列リテラル、アノテーション遅延評価等） | [Python.org](https://www.python.org/downloads/) |

## Deep Dive

- [TypeScript 6.0 RC — JS ベース最後のメジャーリリース](./tu-typescript-6-0-rc.md)
