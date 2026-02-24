# Tech Updates — 2026-02-24

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 Beta リリース | JavaScript ベースの最後のリリース。strict モードがデフォルト有効化、ES5 ターゲット・AMD/UMD モジュール非推奨化。Go リライト版 7.0 への橋渡し | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/) |
| 2 | Go | 1.26 リリース | 2つの言語仕様変更、`new` 関数が初期値式を受付可能に。新パッケージ `crypto/hpke`（RFC 9180）、実験的 `simd/archsimd` パッケージ追加 | [公式ブログ](https://go.dev/blog/go1.26) |
| 3 | Astro | 6 Beta リリース | Vite Environment API ベースの開発サーバー刷新、Cloudflare Workers ファーストクラスサポート、CSP 安定化、Live Content Collections 安定化 | [公式ブログ](https://astro.build/blog/astro-6-beta/) |
| 4 | Deno | 2.6 リリース | `dx`（npx 相当）導入、`tsgo` 統合による高速型チェック、`deno audit` コマンド追加、権限のより細かい制御 | [公式ブログ](https://deno.com/blog/v2.6) |
| 5 | Tailwind CSS | 4.2.0 リリース | webpack プラグイン追加、新カラーパレット4種（mauve/olive/mist/taupe）、ブロック方向の論理プロパティユーティリティ、`font-features-*` ユーティリティ追加 | [GitHub](https://github.com/tailwindlabs/tailwindcss/releases) |
| 6 | Cursor | 2.5 リリース | プラグインシステムとマーケットプレイス導入。Amplitude, AWS, Figma, Stripe 等のプリビルトプラグイン提供。サブエージェント機能改善 | [公式ブログ](https://cursor.com/blog/marketplace) |
| 7 | VS Code | 1.110（February 2026） | チャット会話のフォーク機能、Claude Agent の MCP サーバーサポート、ターミナル OSC 99 デスクトップ通知対応 | [リリースノート](https://code.visualstudio.com/updates/v1_110) |
| 8 | PostgreSQL | 臨時リリース（2/26 予定） | 2/12 の更新リリース（18.2, 17.8, 16.12, 15.16, 14.21）で発生したリグレッションの修正 | [公式](https://www.postgresql.org/about/news/out-of-cycle-release-scheduled-for-february-26-2026-3241/) |
| 9 | Waku | 1.0 Alpha リリース | ミニマルな React フレームワークが Alpha 到達。Vite + Hono ベース、パブリック API の安定化。エントリファイルのリネーム（破壊的変更） | [公式ブログ](https://waku.gg/blog/waku-v1-alpha) |
| 10 | Bun | 1.3.8 リリース | `Bun.markdown`（Zig 実装の CommonMark パーサー）追加、バンドラに `--metafile-md`（LLM フレンドリーなモジュールグラフメタデータ）追加 | [公式ブログ](https://bun.com/blog) |

## Deep Dive

- [TypeScript 6.0 Beta — JavaScript ベース最後のリリース](./tu-typescript-6-beta.md)
- [Deno 2.6 — dx, tsgo, deno audit で開発体験を大幅強化](./tu-deno-2-6.md)
