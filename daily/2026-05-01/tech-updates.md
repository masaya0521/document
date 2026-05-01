# Tech Updates — 2026-05-01

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | pnpm | 11.0 リリース | サプライチェーン保護をデフォルト化、Node.js 22 必須、純粋 ESM 化、ストアを SQLite ベースに刷新。設定は `pnpm-workspace.yaml` に集約 | [InfoQ](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/) / [pnpm Blog](https://pnpm.io/blog/releases/11.0) |
| 2 | Kubernetes | v1.36 リリース (2026-04-22) | SELinux ボリュームラベリング GA、ServiceAccount トークンの外部署名対応、DRA の taints/tolerations や分割可能デバイス対応。`gitRepo` ボリュームは永久無効化 | [Kubernetes Blog](https://kubernetes.io/blog/2026/03/30/kubernetes-v1-36-sneak-peek/) |
| 3 | Bun | v1.3.13 リリース | `bun test --parallel`/`--isolate`/`--shard`/`--changed` を追加。`bun install` がストリーミング展開で 17x メモリ削減、ソースマップは 8x 削減、zlib-ng で gzip 5.5x 高速化 | [Bun Blog](https://bun.com/blog/bun-v1.3.13) |
| 4 | Deno | v2.7.13 リリース (2026-04-28) | Deno 2.7 系のパッチリリース。Deno 2.7 では Temporal API 安定化・Windows on ARM 対応・`package.json` の npm overrides・Brotli ストリーム・`deno create` 等を導入 | [GitHub Releases](https://github.com/denoland/deno/releases/tag/v2.7.13) |
| 5 | Astro | 6.1.7 リリース (2026-04-15) | Netlify 静的ビルド時のリモート画像寸法検証、Vite 再起動後の `--port` フラグ、`/_image` エンドポイントの `f=svg` パラメータ問題を修正 | [GitHub Releases](https://github.com/withastro/astro/releases) |
| 6 | Vue.js | 3.6.0-beta.10 (2026-04-13) | Vapor Mode 実用化に向けたベータ更新。VDOM を介さないコンパイル戦略で Solid/Svelte 級のパフォーマンスを目指す | [GitHub Releases](https://github.com/vuejs/core/releases) |
| 7 | Tailwind CSS | v4.2.4 (2026-04-21) | `@tailwindcss/vite` で Vite alias 解決時の `@import` / `@plugin` 不具合を修正。直前の v4.2.3 では `tracking-*` の正規化を改善 | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases) |
| 8 | Python | 3.15.0a8 / 3.14.4 / 3.13.13 リリース | 3.15 は α8 でプレリリース継続（次回 b1 は 2026-05-05 予定）。3.14.4 は約 337 件のバグ修正・ドキュメント改善を含むメンテナンスリリース | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/) |
| 9 | VS Code | 1.117 (2026-04-22) | Autopilot（完全自律エージェントセッション）パブリックプレビュー、ブラウザデバッグ統合、チャット内画像/動画対応、エージェント権限プロファイル（Default / Bypass Approvals / Autopilot） | [VS Code Updates](https://code.visualstudio.com/updates) |
| 10 | GitHub Copilot | データレジデンシー (US/EU) と FedRAMP 対応モデル GA (2026-04-13) | Copilot の推論処理と関連データを指定地域内に留められるように。FedRAMP 認可済みモデルも利用可能に | [GitHub Changelog](https://github.blog/changelog/2026-04-13-copilot-data-residency-in-us-eu-and-fedramp-compliance-now-available/) |

## Deep Dive

- [pnpm 11.0 — サプライチェーン保護がデフォルトになった大型リリース](./tu-pnpm-11.md)
- [Kubernetes v1.36 — DRA 強化と ServiceAccount トークン外部署名](./tu-kubernetes-1-36.md)
