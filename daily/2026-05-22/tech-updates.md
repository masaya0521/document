# Tech Updates — 2026-05-22

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Ruby | 4.0.5 リリース | `pthread` ベースの `getaddrinfo` タイムアウトハンドラに Use-after-free 脆弱性 (CVE-2026-46727) を修正。4.0.4 で混入していた C ロケール環境下のビルド回帰も解消 | [Ruby News](https://www.ruby-lang.org/en/news/2026/05/20/ruby-4-0-5-released/) |
| 2 | Visual Studio Code | 1.121 リリース | Markdown プレビュー/Notebook で Mermaid を組み込みレンダリング、ローカル HTML ファイルを統合ブラウザで拡張不要にプレビュー。SSH / Dev Tunnels 経由でエージェントセッションをリモート実行可能に | [Release Notes](https://code.visualstudio.com/updates/v1_121) |
| 3 | Visual Studio | 2026 May update | AI プラットフォーム統合を本格化した「新時代」の最初のアップデート。コア性能と AI ツール連携を強化 | [Release Notes](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 4 | GitHub Copilot | GPT-5.3-Codex を Business/Enterprise の既定 LTS モデルに | 5/17 から Copilot Business / Enterprise の Org 全体で GPT-5.3-Codex が既定モデル化。初の LTS モデルで launch 日から 12 ヶ月の可用性保証 | [Changelog](https://github.blog/changelog/) |
| 5 | PostgreSQL | 18.4 / 17.10 / 16.14 / 15.18 / 14.23 同時リリース | 65 件以上のバグ修正を含む定例マイナー。`tzdata` を 2026b へ更新。LTS の 14 系もカバーしているため早期適用が推奨 | [Release Notes](https://www.postgresql.org/docs/release/) |
| 6 | Bun | v1.3.14 リリース | 組み込み画像処理 API と実験的な HTTP/3 サポートを追加。前日の 1.3.13 では `bun test --parallel/--isolate/--shard/--changed`、`bun install` のストリーミングインストール (メモリ 17 倍削減)、`zlib-ng` による 5.5 倍高速 gzip など多数の DX 改善 | [Bun Blog](https://bun.com/blog) |
| 7 | Angular | 21.2.13 リリース & 22.0.0-rc.0 | 同日に 21 系の最新パッチと 22 系の最初の RC が登場。21 系は Esbuild 既定化と Vitest 既定化を完了させた版で、22 系の安定版は 5 月後半に予定 | [Releases](https://github.com/angular/angular/releases) |
| 8 | Docker | Docker AI Governance を発表 | エージェントの実行範囲・到達可能なネットワーク・利用可能な資格情報・呼び出せる MCP ツールを一括制御する企業向け統制機能 | [Docker Blog](https://www.docker.com/blog/) |
| 9 | Tailwind CSS | v4.3 リリース | 一次対応のスクロールバースタイリング、追加の logical property ユーティリティ、`zoom`/`tab-size` ユーティリティ、`@variant` 改善を追加 | [Releases](https://github.com/tailwindlabs/tailwindcss/releases) |
| 10 | Python | 3.14.5 リリース (RC1 を経て final 5/8) | 3.14.0〜3.14.4 で導入された増分 GC を本番環境のメモリ圧迫報告を受けて 3.13 の世代別 GC へ巻き戻し。約 113 件のバグ修正・ビルド改善・ドキュメント更新 | [Python Insider](https://blog.python.org/2026/05/python-3145rc1/) |

## Deep Dive

- [VS Code 1.121 — Mermaid / HTML プレビューと Remote Agent](./tu-vscode-1-121.md)
- [Python 3.14.5 — 増分 GC ロールバックと「やってみたが本番で詰まった」教訓](./tu-python-3-14-5.md)

## 補足: 月内に出た主な周辺アップデート (5/1–5/15)

- **Go 1.26.3 / Go 1.25.10** (5/7): `go` コマンド、`pack` ツール、複数パッケージへのセキュリティ修正と多数のバグ修正
- **Next.js 16.2.6** (5/7): 16 系の最新パッチ。CVE-2026-23869 を含むセキュリティ修正をバックポート
- **Rust 1.96.0 beta** (4/28 分岐): stable は 5/28 リリース予定
- **Tailscale Terraform Provider 0.29.0**: Tailscale Services 管理、Terraform plugin framework への移行
