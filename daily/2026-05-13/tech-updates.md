# Tech Updates — 2026-05-13

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Python | 3.15 beta 1 | フィーチャーフリーズ。lazy imports / free-threaded CPython の安定 ABI / 新サンプリングプロファイラ / JIT 高速化が確定。10/1 正式版に向けてベータフェーズ入り | [The Register](https://www.theregister.com/devops/2026/05/11/feature-freeze-for-python-315-as-first-beta-released/), [PEP 790](https://peps.python.org/pep-0790/) |
| 2 | Python | 3.14.5 | 3.14 系の 5 番目のメンテナンスリリース。バグ修正中心 | [Python Insider](https://blog.python.org/2026/05/python-3145rc1/) |
| 3 | Go | 1.25.10 / 1.26.3 | 同日に両系列でセキュリティパッチ。`go` コマンド、`pack`、`html/template`、`net/http`、`net/url`、`syscall` などの脆弱性修正 | [Go release history](https://go.dev/doc/devel/release) |
| 4 | Bun | 1.3.13 | `bun test --parallel` / `--isolate` / `--shard` / `--changed` を追加。`bun install` のメモリ使用量が 1/17 に。gzip が zlib-ng で 5.5x 高速化 | [Bun Blog](https://bun.com/blog/bun-v1.3.13) |
| 5 | Bun | 1.3.12 | ターミナルでの Markdown レンダリング（`bun ./file.md`）、`Bun.WebView` ヘッドレスブラウザ自動化、in-process `Bun.cron()`、ネイティブエラーの async stack traces | [Bun Blog](https://bun.com/blog) |
| 6 | Rust | 1.95.0 | `cfg_select!` マクロ（cfg-if 相当の条件分岐を組込）、if let guards の安定化、新たに安定化された API 群 | [Rust Blog](https://blog.rust-lang.org/2026/04/16/Rust-1.95.0/) |
| 7 | Kubernetes | 1.33.11 | 1.33 系の最終局面パッチリリース。1.33 は 2026-06-28 で EOL、4/28 からメンテモード | [Kubernetes Releases](https://kubernetes.io/releases/) |
| 8 | Next.js | 16.2 | dev サーバ起動が ~400% / レンダリングが ~50% 高速化、Turbopack 200+ バグ修正、SRI 対応、AGENTS.md を `create-next-app` に追加 | [Next.js Blog](https://nextjs.org/blog) |
| 9 | Tailwind CSS | 4.2.2 | Vite 8 を正式サポート。`@tailwindcss/vite` を Rolldown ベースの Vite 8 でも利用可能に | [GitHub Discussions](https://github.com/tailwindlabs/tailwindcss/discussions/19624) |
| 10 | Vite | 8.0.0 | デフォルトバンドラを Rust 製の Rolldown に統一。esbuild 比で 10–30x 高速化、既存 Rollup/Vite プラグインは概ね互換 | [Vite Blog](https://vite.dev/blog/announcing-vite8) |

## Deep Dive

- [Python 3.15 beta 1 — フィーチャーフリーズと 4 つの大きな変化](./tu-python-3-15-beta1.md)
- [Bun 1.3.13 — `bun test` がついに parallel / isolate を獲得](./tu-bun-1-3-13.md)
