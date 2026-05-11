# Tech Updates — 2026-05-12

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Node.js | v26.0.0 リリース | Temporal API がデフォルト有効化、V8 14.6 / Undici 8.0 へ更新、新 Current ライン | [公式ブログ](https://nodejs.org/en/blog/release/v26.0.0) |
| 2 | Node.js | v26.1.0 リリース | 実験的 `node:ffi` モジュールが追加、JS から動的ライブラリ・ネイティブシンボル呼び出しが可能に | [Releases](https://github.com/nodejs/node/releases) |
| 3 | Python | 3.14.5 リリース | 3.14 系の5回目メンテナンスリリース、約154件のバグ修正・ビルド改善・ドキュメント更新 | [Release](https://www.python.org/downloads/release/python-3145/) |
| 4 | Go | 1.25.10 リリース | `go` コマンド / `html/template` / `net` / `net/http` 等のセキュリティ修正、コンパイラ・リンカ・ランタイムのバグ修正 | [Release History](https://go.dev/doc/devel/release) |
| 5 | Redis | 6.2.22 リリース | CVE-2026-25243（`RESTORE` の不正メモリアクセスによる RCE 可能性）修正、`SUBSCRIBE` 系・`SCRIPT DEBUG` のクラッシュ修正 | [Releases](https://github.com/redis/redis/releases) |
| 6 | pnpm | v11.x 系継続更新 | ESM 化と Node.js 22+ 必須、`minimumReleaseAge` デフォルト 1 日、SBOM 生成、SQLite ストア (v11) | [Releases](https://github.com/pnpm/pnpm/releases) |
| 7 | Docker Desktop | 5月リリース | Logs ビュー GA、Windows でユーザ単位/全ユーザインストールの選択、CVE-2026-31431 / CVE-2026-33990 修正、RHEL 8 サポート終了 | [Release Notes](https://docs.docker.com/desktop/release-notes/) |
| 8 | GitHub Copilot in VS Code | 4月リリース総括 | Copilot CLI セッションのリモート制御、セマンティックなコードベース検索、エンタープライズ向け制御強化、トークン使用量削減 | [GitHub Changelog](https://github.blog/changelog/2026-05-06-github-copilot-in-visual-studio-code-april-releases/) |
| 9 | Bun | v1.3.13 リリース | 82件のバグ修正、`bun test --parallel/--isolate/--shard/--changed`、`bun install` 中のメモリ 17 倍削減、5.5 倍高速な gzip、SHA3 サポート | [Bun Blog](https://bun.com/blog/bun-v1.3.13) |
| 10 | Tailwind CSS | v4.2.4 リリース | `@tailwindcss/vite` で Vite alias 利用時の `@import` / `@plugin` 解決を修正 | [Releases](https://github.com/tailwindlabs/tailwindcss/releases) |

## Deep Dive

- [Node.js 26 — Temporal API デフォルト有効化と node:ffi 追加](./tu-nodejs-26.md)
- [pnpm 11 — サプライチェーン防御のための minimumReleaseAge と Store v11](./tu-pnpm-11.md)
