# Tech Updates — 2026-05-03

開発者が日常的に使う技術そのもののアップデート情報を10件厳選。フレームワーク・ランタイム・パッケージマネージャ・言語・インフラツールのリリースを横断的にカバー。

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | pnpm | v11.0 リリース | SQLite ベースの新ストアフォーマット、ネイティブ publish、ESM 化、Node.js 22+ 必須、`minimumReleaseAge=1440` などサプライチェーン保護がデフォルト ON | [InfoQ](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/) / [pnpm Blog](https://pnpm.io/blog/releases/11.0) |
| 2 | Bun | v1.3.13 リリース | `bun test --isolate/--parallel/--shard/--changed`、`bun install` がストリーミング展開でメモリ 17x 削減、source map 8x 削減、gzip 5.5x 高速化、SHA3、`Bun.serve()` の Range request 対応 | [Bun Blog](https://bun.com/blog/bun-v1.3.13) |
| 3 | VS Code | 1.117 リリース | BYOK（Business/Enterprise 向けカスタムモデル）、incremental chat rendering、ターミナルから Copilot CLI 起動、TypeScript 6.0.3 同梱 | [VS Code Updates](https://code.visualstudio.com/updates/v1_117) / [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/04/23/visual-studio-code-1-117-expands-copilot-controls-for-business-and-enterprise-user.aspx) |
| 4 | VS Code | 1.116 リリース | Agent Debug Logs、Copilot CLI thinking effort 設定、ターミナル agent tools、GitHub Copilot 拡張のビルトイン化 | [VS Code Updates](https://code.visualstudio.com/updates/v1_116) |
| 5 | Astro | 6.2 リリース / 7 alpha プレビュー | 6.2 で実験的カスタムロガー（JSON 出力）・SVG 最適化 API・font URL ヘルパー追加。7 alpha は Vite 8 サポートと Rust コンパイラ stable のプレビュー | [Astro Blog](https://astro.build/blog/whats-new-april-2026/) |
| 6 | SvelteKit / sv | 2026-05 アップデート | SvelteKit の remote functions 大幅改善、TypeScript 6.0 サポート、Svelte CLI が community add-ons を実験的サポート（`sv@0.1.0`）、`sv` と `sv-utils` 分離（`sv@0.2.0`） | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-may-2026) |
| 7 | Python | 3.14.4 / 3.15.0a8 リリース | 3.14.4 は 337 件のバグ修正・ドキュメント改善を含むメンテナンスリリース（4/7）。3.15.0 alpha 8 も同日公開、5/5 に beta 1 が予定され feature freeze 入り | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/) |
| 8 | Go | 1.26.2 セキュリティリリース | `go` コマンド・コンパイラ・`archive/tar`・`crypto/tls`・`crypto/x509`・`html/template`・`os` のセキュリティ修正を含むパッチ（4/7） | [Go Release History](https://go.dev/doc/devel/release) |
| 9 | Kubernetes | v1.36 リリース予定 | 4/22 に v1.36 リリース予定。多数の enhancement と deprecation を含むメジャーマイナー。次期 v1.34 patch（1.34.6）は 3/19 公開済み | [Kubernetes Releases](https://kubernetes.io/releases/) / [v1.36 Sneak Peek](https://kubernetes.io/blog/2026/03/30/kubernetes-v1-36-sneak-peek/) |
| 10 | GitHub Copilot CLI | v1.0.40 リリース | アシスタント応答のスムーズなストリーミング、MCP サーバー向け `client_credentials` OAuth 対応（ヘッドレス認証）、prompt mode の repo hooks/workspace MCP オプトイン化（secure-by-default） | [GitHub Releases](https://github.com/github/copilot-cli/releases) |

## Deep Dive

- [pnpm 11.0 — SQLite ストア・ESM 化・サプライチェーン保護のデフォルト ON](./tu-pnpm-11.md)
- [Bun v1.3.13 — テスト isolation/parallel と install のメモリ 17x 削減](./tu-bun-1-3-13.md)
