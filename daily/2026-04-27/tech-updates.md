# Tech Updates — 2026-04-27

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 7.0 Beta（2026-04-21） | コンパイラを Go に移植した「Project Corsa」が初の公開ベータ。`tsgo` で tsc と並走でき、VS Code リポジトリで tsc 78 秒 → tsgo 7.5 秒と約10倍高速。`@typescript/native-preview@beta` で配布。 | [Microsoft Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/04/21/typescript-7-0-beta-arrives-on-go-based-foundation-with-10x-speed-claim.aspx) |
| 2 | Bun | v1.3.13（2026-04-19） | `bun test` に `--parallel` / `--isolate` / `--shard` / `--changed` を追加。`bun install` がストリーム展開で 17倍メモリ削減、ソースマップは 8倍削減。`zlib-ng` で gzip が 5.5倍速、`Bun.serve()` の Range リクエスト対応など。82 issue 修正。 | [Bun Blog](https://bun.com/blog/bun-v1.3.13) |
| 3 | VS Code | v1.116（2026-04-15） | チャット内に diff を直接描画、ストリーミング時のレイアウトスラッシング削減で応答が高速化。エージェントのデバッグログ、Copilot CLI の thinking effort 制御、ターミナルエージェントツールが追加。 | [Release Notes](https://code.visualstudio.com/updates/v1_116) |
| 4 | Next.js | 16.2 | React アップグレード、Turbopack の Fast Refresh / WASM Workers / Subresource Integrity / 動的 import の tree-shaking、実験的ルーティング強化、型チェック厳格化、200+ の修正。 | [Releasebot 集約](https://releasebot.io/updates/vercel/next-js) |
| 5 | Svelte / SvelteKit | 2026年4月アップデート | OpenCode 設定が `sv` の `.opencode/` に統合、`svelte.config.js` で関数によるオプション設定、`svelte/motion` の型追加、SvelteKit のサーバ側 error boundary、`$app/types` での matcher 型ナローイング。 | [What's new in Svelte April 2026](https://svelte.dev/blog/whats-new-in-svelte-april-2026) |
| 6 | Astro | 6.1.7（2026-04-15） | リモート画像のサイズ検証漏れ修正、`/_image` エンドポイントが任意の `f=svg` クエリで非 SVG を `image/svg+xml` として配信していた問題を修正（SVG であることを検証するよう変更）。セキュリティ寄りの fix を含む。 | [GitHub Releases](https://github.com/withastro/astro/releases) |
| 7 | Go | 1.26.2 / 1.25.9（2026-04-07） | `go` コマンド・コンパイラ・`archive/tar` / `crypto/tls` / `crypto/x509` / `html/template` / `os` のセキュリティ修正、`go fix` ・リンカ・ランタイム・`net` / `net/http` のバグ修正を含むセキュリティリリース。 | [Go Release History](https://go.dev/doc/devel/release) |
| 8 | Python | 3.14.4 / 3.15.0a8（2026-04-07） | 3.14 系 4 回目のメンテナンスリリースで約 337 のバグ修正・ビルド改善・ドキュメント更新。3.15 は引き続き alpha（最終 GA は 2026-10 予定）。 | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/) |
| 9 | pnpm | 11 Release Candidate | SQLite ベースの新ストアフォーマット、`minimumReleaseAge`（依存関係クールダウン）のデフォルト化などサプライチェーン防御を強化、ビルドスクリプト設定の統合、グローバルインストールの隔離、Node.js v22+ 必須に。 | [InfoQ](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/) |
| 10 | FastAPI | 0.136.1（2026-04-23） | 2026-04-16 の 0.136.0 に続くパッチ。Python 3.10 以降が必須となり、新規プロジェクトでピン推奨される版。 | [GitHub Releases](https://github.com/fastapi/fastapi/releases) |

## Deep Dive

- [TypeScript 7.0 Beta — Go 製コンパイラと 10倍高速化の中身](./tu-typescript-7-0-beta.md)
- [Bun v1.3.13 — テストランナー強化とメモリ効率の大幅改善](./tu-bun-1-3-13.md)
