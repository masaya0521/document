# Tech Updates — 2026-05-09

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | React / Next.js | RSC 脆弱性パッチリリース | React `19.0.6` / `19.1.7` / `19.2.6`、Next.js `15.5.16` / `16.2.5` を含む RSC 関連の DoS 脆弱性向け修正がアナウンスされ、Cloudflare WAF も同日マネージドルールを更新 | [Cloudflare Changelog](https://developers.cloudflare.com/changelog/post/2026-05-06-react-nextjs-vulnerabilities/) |
| 2 | React | v19.2.6 リリース | 型ハードニングとパフォーマンス改善を含む 19.2 系の最新パッチ。19.2 で導入された新 `useId` プレフィックスや `Activity` の visible/hidden モードを引き継ぐ | [React Versions](https://react.dev/versions) |
| 3 | Python | 3.14.5 final リリース | 3.14 系の 5 つ目のメンテナンスリリース。3.14.4 以降のバグ修正・ビルド改善・ドキュメント更新を取り込んだ最終版 | [Python Insider](https://blog.python.org/2026/05/python-3145rc1/) |
| 4 | Go | 1.25.10 リリース | 1.25 系のメンテナンスリリース。Green Tea GC が既定化された Go 1.26 系の前世代としてセキュリティ・バグ修正を継続的に提供 | [Go Release History](https://go.dev/doc/devel/release) |
| 5 | SvelteKit | 2.56 / 2.57 リリース | TypeScript 6.0 サポート、フォームフィールドのデフォルト値指定、リモート関数トランスポートの改善を含む 5 月の連続リリース | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-may-2026) |
| 6 | Vercel CLI | `vercel metrics` ベータ提供開始 | Observability Plus のメトリクスを CLI から問い合わせ可能になり、CI/CD パイプラインや運用スクリプトからプロジェクトの可観測性データを直接取得できる | [Vercel Changelog](https://vercel.com/changelog) |
| 7 | Vercel Flags | JSON 値のサポート追加 | これまで boolean / string / number だったフラグ値に JSON が加わり、関連する複数フラグを 1 つに集約できるようになった | [Vercel Changelog](https://vercel.com/changelog) |
| 8 | Vercel Sandbox | ホスト型 Postgres 接続対応 | Sandbox の許可ドメインに DB ホストを追加することで Neon / Supabase / AWS RDS / Nile / Prisma Postgres へ直接接続可能になった | [Vercel Changelog](https://vercel.com/changelog) |
| 9 | pnpm | v11.0 GA リリース | パッケージインデックスを SQLite 化、pnpm 本体が pure ESM に移行、`minimumReleaseAge` 既定 1 日 / `blockExoticSubdeps` 既定 true でサプライチェーン保護を強化、Node.js 22+ を要件化 | [pnpm Blog](https://pnpm.io/blog/releases/11.0) |
| 10 | Bun | v1.3.13 リリース | `bun test --parallel` / `--isolate` / `--shard` / `--changed` の追加、`bun install` のメモリ使用量 17 倍削減、zlib-ng 採用で gzip が 5.5 倍高速化 | [Bun Blog](https://bun.com/blog) |

## Deep Dive

- [pnpm 11.0 — SQLite ストアと既定セキュリティ強化](./tu-pnpm-11.md)
- [React Server Components 脆弱性パッチ群（2026-05-06）](./tu-react-nextjs-rsc-patch.md)

## ソース一覧

- [Cloudflare Changelog — WAF and framework adapter mitigations for React and Next.js vulnerabilities](https://developers.cloudflare.com/changelog/post/2026-05-06-react-nextjs-vulnerabilities/)
- [React Versions](https://react.dev/versions)
- [React 19.2 リリースブログ](https://react.dev/blog/2025/10/01/react-19-2)
- [Python Insider — 3.14.5rc1](https://blog.python.org/2026/05/python-3145rc1/)
- [Go Release History](https://go.dev/doc/devel/release)
- [Svelte Blog — What's new in May 2026](https://svelte.dev/blog/whats-new-in-svelte-may-2026)
- [Vercel Changelog](https://vercel.com/changelog)
- [pnpm 11.0 リリースノート](https://pnpm.io/blog/releases/11.0)
- [Bun Blog](https://bun.com/blog)
