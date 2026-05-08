# Tech Updates — 2026-05-08

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Bun | v1.3.13 リリース | `bun test` に `--parallel` / `--isolate` / `--shard` / `--changed` 追加。`bun install` がストリーム展開で 17x メモリ削減、ソースマップ 8x 削減、zlib-ng で gzip 5.5x 高速化 | [Bun Blog](https://bun.com/blog/bun-v1.3.13) |
| 2 | Rust | 1.95.0 リリース | `if let` ガードを match 式で安定化、`cfg_select!` マクロ追加、Cargo が TOML v1.1 を解釈、stable での custom target spec を削除 | [Rust Blog](https://blog.rust-lang.org/2026/04/16/Rust-1.95.0/) |
| 3 | Node.js | 24.15.0 LTS リリース | Node.js 24 系が LTS 入り（〜2028年4月）。OpenSSL 3.5、デフォルト security level 2、RC4 廃止、Buffer 書き込み境界チェック厳格化 | [Node.js](https://nodejs.org/en/blog/release/v24.15.0) |
| 4 | Kubernetes | v1.36 "Haru" リリース | 70 enhancements（Stable 18 / Beta 25 / Alpha 25）。SELinux ボリュームマウント改善が GA、`mount -o context=` で Pod 起動高速化 | [Kubernetes](https://kubernetes.io/blog/2026/04/22/kubernetes-v1-36-release/) |
| 5 | Astro | 6.0 安定版リリース | Vite Environment API ベースに dev サーバー全面刷新、CSP / Live Content Collections / Fonts API 安定化、experimental Rust compiler 同梱 | [Astro Blog](https://astro.build/blog/astro-6/) |
| 6 | Redis | 8.6.3 リリース | バグ修正・安定化を中心としたパッチリリース | [Redis Releases](https://github.com/redis/redis/releases) |
| 7 | Python | 3.14.5 RC1 リリース | 3.14 系のメンテナンスリリース候補。バグ修正中心 | [Python Insider](https://blog.python.org/2026/05/python-3145rc1/) |
| 8 | Docker Engine | 5月リリース | Docker Engine 系最新パッチがリリース。修正・セキュリティ更新中心 | [Docker Docs](https://docs.docker.com/engine/release-notes/) |
| 9 | GitHub Copilot CLI | v1.0.42 リリース | MCP server 障害時の警告改善、UI 即時描画による起動高速化 | [GitHub Copilot CLI](https://github.com/github/gh-copilot/releases) |
| 10 | GitHub Copilot in VS Code | v1.116-v1.119 (4月〜5月リリース) | `/chronicle` で過去のチャット履歴・触ったファイル・参照した PR を呼び戻す実験機能、エージェントへのインライン diff・ブラウザタブ共有・ターミナル read/write、BYOK の Business/Enterprise 拡張 | [GitHub Changelog](https://github.blog/changelog/2026-05-06-github-copilot-in-visual-studio-code-april-releases/) |

## Deep Dive

- [Bun v1.3.13 — テストランナーとインストーラの大幅改善](./tu-bun-1-3-13.md)
- [Rust 1.95 — `if let` ガードと `cfg_select!` の安定化](./tu-rust-1-95.md)
