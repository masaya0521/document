# Tech Updates — 2026-05-07

開発者の日常業務に直結する技術アップデートを 10 件厳選。本日は Bun の Zig→Rust 移植検討、Python 3.15 β1 の Feature Freeze、TypeScript 7.0 Beta、PostgreSQL 計画外リリース予告など、ランタイム／言語まわりの動きが目立つ。

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Bun | Zig → Rust 移植ガイド公開 (2026-05-05) | `docs/PORTING.md` を公開し、coding agent 向けに移植手順を整備。コミット文には「rewrite はまだ half-baked」とあり、正式採用は未確定 | [The Register](https://www.theregister.com/2026/05/05/bun_rust_port/) |
| 2 | Python | 3.15.0 beta 1 リリース (Feature Freeze, 2026-05-05) | 3.15 系の Feature Freeze。新機能追加はここで打ち止めとなり、以降は安定化フェーズへ | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/) |
| 3 | Python | 3.14.5 メンテナンスリリース (予定: 2026-05-08) | 3.14 系の通常メンテナンスリリース。バグ修正・セキュリティ修正中心 | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/) |
| 4 | PostgreSQL | 18.1, 17.7, 16.11, 15.15, 14.20, 13.23 計画外リリース (予定: 2026-05-14) | スタンバイがトランザクション status エラーで停止する不具合、`substring()` の `invalid byte sequence` エラー（CVE-2026-2006 修正のリグレッション）、`json_strip_nulls` / `jsonb_strip_nulls` の volatility を IMMUTABLE に修正（インデックス利用可） | [PostgreSQL News](https://www.postgresql.org/about/news/postgresql-181-177-1611-1515-1420-and-1323-released-3171/) |
| 5 | TypeScript | 7.0 Beta 公開 (2026-04-21) | Project Corsa による Go 製ネイティブコンパイラの Beta 公開。tsc 6.0 比で約 10× 高速化を主張。型チェックロジックは 6.0 と構造的に同一 | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/) |
| 6 | Vite | 8.0.10 リリース (2026-04-23) | Vite 8 系のパッチリリース。Rolldown ベースに移行した 8.0 系の安定化パッチが継続中 | [vitejs/vite Releases](https://github.com/vitejs/vite/releases) |
| 7 | Bun | v1.3.12 リリース (2026-04-19) | 1.3 系の継続パッチ。直近の 1.1.13 で Anthropic 主導のメモリリーク修正を取り込み、企業利用での安定性が改善 | [oven-sh/bun Releases](https://github.com/oven-sh/bun/releases) |
| 8 | Docker Desktop | 4.70.0 リリース (2026-04-20) | Kubernetes pod discovery が context 不通時にハングする不具合を修正、hostPath volume mount の Linux ホスト失敗を解消、kind ベースのクラスタが新規デフォルトに継続採用 | [Docker Desktop Release Notes](https://docs.docker.com/desktop/release-notes/) |
| 9 | Deno | 2.7.14 リリース (April 2026) | 2.7 系のパッチ継続。Temporal API 安定化、npm 互換性、TypeScript ネイティブ実行を維持 | [denoland/deno Releases](https://github.com/denoland/deno/releases) |
| 10 | Go | 1.26.2 リリース (2026-04-07) | go1.26 系のセキュリティ修正＋バグ修正リリース。1.26 自体は 4 月初旬に公開済 | [Go Release History](https://go.dev/doc/devel/release) |

## Deep Dive

- [Bun: Zig → Rust 移植検討の波紋](./tu-bun-zig-to-rust-port.md)
- [TypeScript 7.0 Beta: Project Corsa による Go 製コンパイラ](./tu-typescript-7-0-beta.md)

## 参考: 関連動向

- **CVE-2026-23864 / CVE-2026-23869**: React Server Components / Server Functions の DoS 脆弱性。Next.js 13.x〜16.x、`react-server-dom-{webpack,parcel,turbopack}` 19.0.0〜19.2.3 が影響。認証なしで悪用可能なため、未パッチ環境は早期アップグレード推奨 ([React Blog](https://react.dev/blog/2025/12/11/denial-of-service-and-source-code-exposure-in-react-server-components), [Vercel Changelog](https://vercel.com/changelog/summary-of-cve-2026-23869))
- **Next.js 16.2** (2026-03-18): dev サーバ起動 87% 高速化、SSR 約 50% 高速化、Turbopack バグ 200+ 修正、AI-Assisted Development 向け機能追加 ([Next.js Blog](https://nextjs.org/blog/next-16-2))
