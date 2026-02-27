# Tech Updates — 2026-02-27

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Go | v1.26 リリース | Green Tea GC がデフォルト有効化、cgo オーバーヘッド 30% 削減、`go fix` の刷新、実験的 SIMD パッケージ追加 | [公式ブログ](https://go.dev/blog/go1.26) |
| 2 | TypeScript | v6.0 Beta リリース | JavaScript ベース最後のリリース。strict モードデフォルト化、ES2025 サポート、Temporal API 追加、ES5/AMD/UMD 非推奨化 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/) |
| 3 | Tailwind CSS | v4.2.0 リリース | webpack プラグイン追加、新カラーパレット4種（mauve, olive, mist, taupe）、論理プロパティユーティリティ拡充 | [Laravel News](https://laravel-news.com/tailwindcss-4-2-0) |
| 4 | Python | v3.14.3 / v3.13.12 リリース | 3.14.3 は約 299 件のバグ修正。3.14 系は free-threaded Python 公式サポート、t-string、Zstandard 圧縮モジュール等を含む | [Python Insider](https://blog.python.org/2026/02/python-3143-and-31312-are-now-available.html) |
| 5 | Rust | v1.93.1 リリース | バグ修正リリース。1.93.0 では musl 1.2.5 更新による DNS リゾルバ改善、インラインアセンブリの cfg 対応、23 API 安定化 | [Rust Blog](https://blog.rust-lang.org/2026/02/12/Rust-1.93.1/) |
| 6 | VS Code | v1.110 (February 2026 Insiders) | チャットプロンプトキューイング、プライベートリポジトリからのエージェントプラグイン導入、従量制ネットワーク検知 | [VS Code Updates](https://code.visualstudio.com/updates/v1_110) |
| 7 | Zed | v0.225.9 リリース | 外部エージェント（Claude Agent, Codex 等）のセッション履歴対応、Mermaid 図サポート、Linux wgpu バックエンド | [Zed Releases](https://zed.dev/releases/stable) |
| 8 | Nuxt | v4.3.1 リリース | v5 機能のオプトイン設定追加。Nuxt Studio のオープンソース化、v3 サポート期間を 2026/7/31 まで延長 | [GitHub Releases](https://github.com/nuxt/nuxt/releases) |
| 9 | Svelte / SvelteKit | v5.47〜5.49 リリース | カスタム `<select>` 要素対応、CSS パーサー（parseCss）のエクスポート、ShadowRootInit サポート | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-february-2026) |
| 10 | Kubernetes | v1.35.1 パッチ / v1.36 Freeze | 1.35.1 パッチリリース。v1.36 は 2/5 に Production Readiness Freeze、2/12 に Enhancements Freeze。4/22 リリース予定 | [Kubernetes](https://kubernetes.io/releases/) |

## Deep Dive

- [Go 1.26 — Green Tea GC・SIMD・go fix 刷新](./tu-go-1-26.md)
- [TypeScript 6.0 Beta — Go リライトへの布石](./tu-typescript-6-beta.md)
