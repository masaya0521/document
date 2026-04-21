# Tech Updates — 2026-04-21

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Node.js | v26 リリース間近（2026-04-22 予定） | 現行リリースモデル下の最後のメジャー。Node.js 27 からは新モデルに移行。2026-10 に LTS 化予定 | [Release Schedule](https://nodejs.org/en/blog/announcements/evolving-the-nodejs-release-schedule) |
| 2 | Kubernetes | v1.36 リリース（2026-04-22 予定） | v1.33 が同日メンテナンスモードに入り EoL は 2026-06-28。v1.36 のスニークピークが公開済み | [v1.36 Sneak Peek](https://kubernetes.io/blog/2026/03/30/kubernetes-v1-36-sneak-peek/) |
| 3 | Deno | v2.5（2026-04-09） | V8 14.0 / TypeScript 5.9.2 アップデート、Permission Sets、test の before/after フック、Bundle ランタイム API | [GitHub Releases](https://github.com/denoland/deno/releases) |
| 4 | Bun | v1.3.13（2026-04） | `bun install` がストリーム展開で 17x メモリ削減、gzip 5.5x 高速化、source map 8x メモリ削減、SHA3 / `ws+unix://` サポート | [Bun Blog v1.3.13](https://bun.com/blog/bun-v1.3.13) |
| 5 | Python | 3.14.4 / 3.15.0a8（2026-04） | 3.14 系の保守リリースと 3.15 の alpha 8。3.15 は次期安定版に向けた新機能追加フェーズ | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/) |
| 6 | JetBrains IDEs | 2026.1（Rider / IntelliJ IDEA / WebStorm） | AI エージェント統合（Codex / Cursor / ACP）、Rider は管理/ネイティブ混在デバッグ、WebStorm はサービス駆動 TS エンジンと Angular 21 対応 | [IntelliJ 2026.1](https://blog.jetbrains.com/idea/2026/03/intellij-idea-2026-1/), [WebStorm 2026.1](https://blog.jetbrains.com/webstorm/2026/03/webstorm-2026-1/) |
| 7 | TypeScript | 6.0（2026-03-23） | JavaScript 実装ベース最後のメジャー。次期 7.0（Corsa）は Go 実装で 5-10x 高速化を謳う | [Announcing TS 6.0](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 8 | Astro | 6.0（2026-03-10） | Vite Environment API 採用、`@astrojs/cloudflare` が開発・SSR 全段階で `workerd` を実行。Node 22 以上必須 | [Astro 6.0 Blog](https://astro.build/blog/astro-6/) |
| 9 | Vite | 8 ベータ / 8.0 リリース（2026 Q1） | Rolldown + Oxc 採用。Dev 起動 3x、full reload 40% 高速化、network request 10x 削減 | [Vite 8 Beta](https://vite.dev/blog/announcing-vite8-beta), [Vite 8.0](https://vite.dev/blog/announcing-vite8) |
| 10 | pnpm | 11.0.0 beta（2026-03-30） | store version を v11 に bump、`docs` / `ping` / `search` コマンド追加。正式版は 4 月後半〜5 月見込み | [GitHub Releases](https://github.com/pnpm/pnpm/releases) |

## Deep Dive

- [TypeScript 6.0 — JavaScript ベース最後のメジャーリリース](./tu-typescript-6-0.md)
- [Node.js 26 — 現行リリースモデル最後のメジャーラインと次世代モデルへの橋渡し](./tu-nodejs-26.md)
