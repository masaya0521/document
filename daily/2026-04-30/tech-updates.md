# Tech Updates — 2026-04-30

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | pnpm | v11.0 リリース | サプライチェーン保護をデフォルト ON、ストアを SQLite 化、ESM 専用、Node 22+ 必須の大規模メジャーリリース | [InfoQ](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/), [pnpm Blog](https://pnpm.io/blog/releases/11.0) |
| 2 | Kubernetes | v1.36 "Haru" リリース | 2026 年最初のメジャーリリースとして 4/22 に GA。次期 v1.37 を見据えた API 安定化とランタイム改善 | [Kubernetes Blog](https://kubernetes.io/blog/2026/04/22/kubernetes-v1-36-release/) |
| 3 | Deno | v2.7.13 リリース | `node:repl` 実装、`node:http` を llhttp + 独自 TCPWrap で書き換え、URLPattern や FFI 等のパフォーマンス改善 | [GitHub Release](https://github.com/denoland/deno/releases/tag/v2.7.13) |
| 4 | Bun | v1.3.13 リリース | `bun test --parallel/--isolate/--shard/--changed`、tarball ストリーミングで `bun install` メモリ 17 倍削減、zlib-ng で gzip 5.5 倍高速化 | [Bun Blog](https://bun.com/blog/bun-v1.3.13) |
| 5 | Node.js | v24.15.0 'Krypton' (LTS) | 5 件の CVE 修正（Web Crypto HMAC タイミング、HTTP/2 フロー制御、URL パース、permission チェック等）、npm を 11.12.1 に更新 | [Node.js Changelog](https://github.com/nodejs/node/blob/main/doc/changelogs/CHANGELOG_V24.md) |
| 6 | Next.js | 16.2.4 LTS リリース | Next.js 16 系の最新 LTS。Turbopack 安定化と PPR、Server Components のバグ修正中心の安定化リリース | [Next.js Blog](https://nextjs.org/blog) |
| 7 | SvelteKit | 2.55 リリース | エンタープライズ向けのハードニング。メモリリーク防止、サーバ側 Error Boundary、`$app/types` での Page/Layout パラメータの型自動絞り込み | [Criztec](https://criztec.com/next-js-16-2-3-sveltekit-2-55-prib/) |
| 8 | Astro | 6.1 リリース | Cloudflare workerd ランタイムとローカル/本番 100% パリティ、Global Image Codecs によるフォーマット標準の強制 | [Criztec](https://criztec.com/next-js-16-astro-6-sveltekit-trade-magic-acsy/) |
| 9 | Python | 3.14.4 / 3.15.0a8 リリース | 3.14 系は 337 件のバグ修正を含む 4 回目のメンテナンスリリース。3.15 は最終 alpha で、5/5 の beta フェーズ入りで新機能追加が締切 | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/) |
| 10 | Go | 1.25.9 / 1.26.1 リリース | `crypto/x509`, `html/template`, `net/url`, `os` 等を中心に 5 件のセキュリティ修正。証明書検証、Path Traversal、URL/IPv6 リテラル検証の堅牢化 | [Heroku Changelog](https://devcenter.heroku.com/changelog-items/3642) |

## Deep Dive

- [pnpm v11.0 — サプライチェーン防御を default に、ストアも刷新した節目のメジャーリリース](./tu-pnpm-11.md)
- [Bun v1.3.13 — テストランナーの parallel/isolate/shard 化と install のメモリ 17 倍削減](./tu-bun-1-3-13.md)
