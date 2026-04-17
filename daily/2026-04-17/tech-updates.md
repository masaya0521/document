# Tech Updates — 2026-04-17

開発者が日常的に使う技術のアップデート情報10件。直近1週間（特に4月上旬〜中旬）のリリースと、4月22日に控えるメジャーリリース（Node.js 26・Kubernetes v1.36）を中心に選定した。

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Rust | v1.95.0 リリース | stable で新機能・ライブラリ安定化を含む定期メジャー（6週サイクル） | [Rust Blog](https://blog.rust-lang.org/2026/04/16/Rust-1.95.0/) |
| 2 | Node.js | v26 リリース予定（2026-04-22） | 偶数メジャー＝10月に Active LTS 昇格の本命リリース。Node.js 25 系から移行 | [docker-node issue](https://github.com/nodejs/docker-node/issues/2435), [Node.js Releases](https://nodejs.org/en/about/previous-releases) |
| 3 | Kubernetes | v1.36 リリース予定（2026-04-22） | 80 機能が enhancement として追跡。HPA の scale-to-zero、gitRepo volume 廃止、IPVS 削除 | [Kubernetes Releases](https://kubernetes.io/releases/), [PerfectScale Sneak Peek](https://www.perfectscale.io/blog/kubernetes-v1-36-sneak-peek) |
| 4 | Python | 3.14.4 / 3.15.0a8 / 3.13.13 リリース（2026-04-07） | 3.14 系に 337 件のバグ修正。3.15 alpha8 で次期機能を継続検証 | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/) |
| 5 | Go | 1.26.2 / 1.25.9 セキュリティリリース（2026-04-07） | go コマンド・compiler・archive/tar・crypto/tls・crypto/x509・html/template・os のセキュリティ修正 | [Go Release History](https://go.dev/doc/devel/release) |
| 6 | TypeScript | v6.0 リリース（2026-03-23） | JS 実装時代の最終メジャー。7.0（Go 実装）への移行準備となる deprecation 多数 | [Announcing TypeScript 6.0](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 7 | Vite | v8.0 リリース（2026-03-12） | Rolldown（Rust 製バンドラー）を統合し build が 10-30x 高速化。2.0 以来の最大級アーキテクチャ変更 | [Vite 8.0 is out!](https://vite.dev/blog/announcing-vite8) |
| 8 | Next.js | v16.2 リリース（2026-03） | 起動時間 ~87% 短縮、Server Components payload のデシリアライズ 350% 高速化、200+ の Turbopack 改善 | [Next.js 16.2](https://nextjs.org/blog/next-16-2) |
| 9 | Tailwind CSS | v4.1 リリース | `text-shadow-*` ユーティリティ、`mask-*` 新 API、`overflow-wrap`、`@source inline(…)` safelist | [Tailwind CSS v4.1](https://tailwindcss.com/blog/tailwindcss-v4-1) |
| 10 | Bun | v1.3.x 継続アップデート | 2025 年 10 月の 1.3（ゼロ設定フロントエンド、Bun.SQL、Redis クライアント内蔵）以降、1.3.3 などパッチ継続 | [Bun 1.3](https://bun.com/blog/bun-v1.3), [Bun 1.3.3](https://bun.com/blog/bun-v1.3.3) |

## Deep Dive

- [TypeScript 6.0 — JS 実装時代の最終リリースと 7.0（Go 実装）への橋渡し](./tu-typescript-6-0.md)
- [Vite 8.0 — Rolldown 統合によるフルリニューアル](./tu-vite-8-0.md)
