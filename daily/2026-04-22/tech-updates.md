# Tech Updates — 2026-04-22

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Node.js | v24.15.0 LTS (Krypton) | V8 13.6 へ更新し `Float16Array` / `Error.isError` / Global `URLPattern` API を追加。Undici v7 で HTTP/2・HTTP/3 対応を強化。サポートは 2028-04-30 まで | [Node.js Previous Releases](https://nodejs.org/en/about/previous-releases), [Vercel Changelog](https://vercel.com/changelog/node-js-24-lts-is-now-generally-available-for-builds-and-functions) |
| 2 | Bun | v1.3.12 | `bun test --parallel / --isolate / --shard / --changed` を追加。`bun install` がタールボールをストリーミングしてメモリ消費を 17 倍削減、zlib-ng で gzip が 5.5 倍高速化。`Bun.serve()` が Range リクエストをサポート | [Bun v1.3.12 Blog](https://bun.com/blog/bun-v1.3.12) |
| 3 | Python | 3.14.4 / 3.15.0a8 / 3.13.13 同時リリース | 3.14.4 は 337 件の bugfix を含むメンテナンス版。XML 解析・HTTP cookies・ファイル読み込みの CVE（2026-4224 / 3644 / 2297）を修正 | [Python Insider Blog](https://blog.python.org/2026/04/python-3150a8-3144-31313/), [Release Notes](https://www.python.org/downloads/release/python-3144/) |
| 4 | Next.js | v16.2.4 | 16.2 の延長線上でのパッチ。App Page の ISR 再検証エラー正常化、`manifest.ts` の HMR 修正、styled-jsx の race condition 解消、Turbopack のキャンセル / エラー処理安定化 | [Next.js Releases](https://github.com/vercel/next.js/releases), [Next.js Changelog](https://next-changelog.vercel.app/) |
| 5 | Tailwind CSS | v4.2.3 | `tracking-*` ユーティリティの canonicalization 改善。candidate に含まれる不正文字によるクラッシュ修正、`@tailwindcss/webpack` で import の query params をサポート | [Tailwind Releases](https://github.com/tailwindlabs/tailwindcss/releases), [Changelog](https://github.com/tailwindlabs/tailwindcss/blob/main/CHANGELOG.md) |
| 6 | Visual Studio | 2026 April Update (17.14) | AI 統合が強化され、Copilot agents がリポジトリ / プロファイルの skill を自動検出。Razor Hot Reload は Roslyn プロセス内に同居する形で高速・堅牢化。JSON エディタが新スキーマ仕様対応 | [VS 2026 Release Notes](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 7 | GitHub Copilot CLI | v1.0.33 | `/bug`, `/continue`, `/release-notes`, `/export`, `/reset` のスラッシュコマンド別名追加。誤入力時に類似コマンドを提案する picker を導入。Claude Opus 4.7 対応、大規模リポでの grep タイムアウト修正 | [Copilot CLI Releases](https://github.com/github/copilot-cli/releases) |
| 8 | GitHub Copilot | Auto model selection GA | 全プランで auto モデル選択が一般提供。効率の良いモデルを Copilot 側で自動選定。使用量が上限に近づくと CLI 上で警告通知 | [Copilot CLI Auto Model](https://github.blog/changelog/2026-04-17-github-copilot-cli-now-supports-copilot-auto-model-selection/) |
| 9 | Deno | 4月9日リリース | TypeScript / core panic 防止 / coverage 改善、Node 互換（TypedArrays、IPv6 multicast）を強化。V8↔Rust 文字列変換・NAPI threadpool・URLPattern・base64 を最適化 | [Deno Releases](https://github.com/denoland/deno/releases) |
| 10 | MySQL | 8.0 EOL 直前（2026-04-30） | 8.0 系は 8.0.46 が最終リリースとして EOL 入り。Oracle は 8.4 LTS への移行を推奨。セキュリティパッチの打ち切りが目前 | [MySQL Release Notes](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/) |

## 参考: Kubernetes 1.33 の EOL

Kubernetes 1.33 は 2026-04-28 にメンテナンスモードへ入り、2026-06-28 に EOL を迎える。1.33 系の最新パッチ 1.33.10 は 2026-03-19 にリリース済み。運用中のクラスタは 1.34 以降への計画的な移行が必要。[Kubernetes Patch Releases](https://kubernetes.io/releases/patch-releases/)

## Deep Dive

- [Node.js 24.15.0 LTS (Krypton) — 主要な変更と移行ポイント](./tu-node-24-15-lts.md)
- [Bun v1.3.12 — テスト並列化と install ストリーミングの威力](./tu-bun-1-3-12.md)
