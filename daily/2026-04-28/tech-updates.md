# Tech Updates — 2026-04-28

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Kubernetes | v1.36 "Haru" リリース（4/22） | 70 機能強化（Stable 18 / Beta 25 / Alpha 25）。ユーザーネームスペース・OCI ボリュームソース・Node ログ検索・変異する管理ポリシー（CEL）が GA。`gitRepo` ボリューム削除、Service `externalIPs` は v1.43 で削除予定 | [リリースブログ](https://kubernetes.io/blog/2026/04/22/kubernetes-v1-36-release/) |
| 2 | Rust | 1.95.0 リリース（4/16） | `cfg_select!` マクロが安定化（cfg-if の置き換え候補）。マッチアームでの `if let` ガード、`Vec::push_mut` / `insert_mut`、Atomic の `update` / `try_update` などが stabilize | [リリースブログ](https://blog.rust-lang.org/2026/04/16/Rust-1.95.0/) |
| 3 | Node.js | 24.15.0 LTS リリース（4/15） | TC39 Explicit Resource Management（`using` / `await using`）を V8 13.6 で標準サポート。Node.js 25 は Current フェーズが 2026-04-01 で終了し EOL（6/1）に向かう | [Node.js リリース履歴](https://nodejs.org/en/about/previous-releases) |
| 4 | Next.js | 16.2.4 LTS リリース（4/16） | 16.2 で Time-to-URL ~400% 改善・rendering ~50% 改善・新 500 ページ。Cache Components（PPR + `use cache`）、Next.js DevTools MCP、`proxy.ts`（middleware.ts の後継）を提供 | [Next.js 16.1 ブログ](https://nextjs.org/blog/next-16-1) |
| 5 | Vite | 8.0.10 リリース（4/23） | rolldown 1.0.0-rc.17 へ更新。Vite 8 は Rolldown ベースのバンドラを採用しビルドパイプラインを統合 | [Vite Releases](https://vite.dev/releases) |
| 6 | Python | 3.14.4 / 3.15.0a8 リリース（4/7） | 3.14.4 は約 337 件の bugfix を含むメンテナンスリリース。3.15 は α 期間が 4 月で終了し、5 月 5 日に β1 を予定 | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/) |
| 7 | Bun | v1.3.12 リリース（4/20） | 安定化路線の継続。Bun 2.0（2026-01）以降の Node.js API 互換改善・組込バンドラ／テストランナーの強化が続く | [Bun Releases](https://github.com/oven-sh/bun/releases) |
| 8 | FastAPI | 0.136.1 リリース（4/23） | **既定で JSON Content-Type ヘッダを検証**（opt-out 可）。Starlette 1.0.0 への bump、Pydantic v2 deprecation 修正 | [FastAPI Release Notes](https://fastapi.tiangolo.com/release-notes/) |
| 9 | pnpm | 11 RC リリース | ESM 配布・サプライチェーンの安全側既定値・新ストアフォーマット。Node 18 EOL 反映と install 性能改善 | [InfoQ](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/) |
| 10 | VS Code | 1.117 リリース（4 月）／GitHub App トークン新形式（4/27〜） | Copilot Enterprise / Business で BYOK・チャットレンダリング改善・TypeScript 復旧修正。GitHub App インストールトークンが新形式に段階移行（4/27〜中旬以降）。Copilot Code Review は 6/1 から Actions 分も消費 | [VS Code 1.117](https://releasebot.io/updates/microsoft/visual-studio-code) ／ [GitHub Changelog](https://github.blog/changelog/2026-04-24-notice-about-upcoming-new-format-for-github-app-installation-tokens/) |

## Deep Dive

- [Rust 1.95.0 — `cfg_select!` 安定化と let chains 由来の if-let ガード](./tu-rust-1-95.md)
- [Kubernetes v1.36 "Haru" — ユーザーネームスペース・OCI ボリューム GA とプロダクション向け新機能](./tu-kubernetes-1-36.md)
