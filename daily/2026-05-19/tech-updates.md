# Tech Updates — 2026-05-19

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Bun | Zig→Rust リライト main にマージ（2026-05-14） | Anthropic が Claude Code エージェントで 6 日間に 96 万行を Rust に移植した PR #30412 が merge。テストスイート 99.8% パス、binary は 3-8 MB 縮小 | [The Register](https://www.theregister.com/devops/2026/05/14/anthropics-bun-rust-rewrite-merged-at-speed-of-ai/5240381) |
| 2 | PostgreSQL | 18.4 / 17.10 / 16.14 / 15.18 / 14.23（2026-05-14） | 11 件のセキュリティ脆弱性と 60 件超のバグ修正。`pg_basebackup` / `pg_rewind` のパストラバーサル、`contrib/spi` の SQL インジェクション等を修正。tzdata 2026b 同梱 | [PostgreSQL News](https://www.postgresql.org/about/news/postgresql-184-1710-1614-1518-and-1423-released-3297/) |
| 3 | VS Code | 1.120（2026-05-13） | Agents window が Stable プレビューに昇格。プラン編集をインライン化、BYOK モデルのトークン使用量制御、ターミナルコマンドのリスクアセスメント等 | [VS Code Updates](https://code.visualstudio.com/updates/v1_120) |
| 4 | Visual Studio | 2026 GA 5月アップデート（2026-05-12） | OS のテーマ変更に追従する Light/Dark 自動切り替えと、Fluent カラートークン単位でテーマをカスタマイズできるオプションページを追加 | [Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 5 | Tailwind CSS | v4.3.0（2026-05-12） | スクロールバー幅・色・gutter 制御を一級ユーティリティ化。`@container-size` の追加、mauve / olive / mist / taupe の 4 パレット、Webpack 用の first-class プラグイン | [Tailwind Blog](https://tailwindcss.com/blog/tailwindcss-v4-3) |
| 6 | Kubernetes | 1.35.5 / 1.34.8 パッチ（2026-05-12） | サポート対象 3 マイナー（1.36 / 1.35 / 1.34）のパッチサイクル。1.34 は 2026-08-27 に保守モード入り | [Kubernetes Patch Releases](https://kubernetes.io/releases/patch-releases/) |
| 7 | Docker | AI Governance（2026-05-12） | エージェントの実行・ネットワーク到達範囲・利用可能なクレデンシャル・MCP ツールを中央集権で管理する企業向け統制機能を発表 | [Docker Blog](https://www.docker.com/blog/docker-terraform-provider/) |
| 8 | Terraform | Docker Terraform Provider（2026-05-12） | Docker 環境（イメージ・コンテナ・ネットワーク等）を Terraform で宣言的に管理する公式プロバイダ。HCP Terraform 連携でセキュア運用を強化 | [Docker Blog](https://www.docker.com/blog/docker-terraform-provider/) |
| 9 | Bun | 1.3.14 リリース | 組み込み画像処理 API `Bun.Image`（Sharp の drop-in）、`fetch()` の HTTP/2・HTTP/3 クライアント、`Bun.serve` での HTTP/3 (QUIC)、isolated linker による warm install 7× 高速化 | [Bun Blog](https://bun.com/blog/bun-v1.3.14) |
| 10 | Django | 6.0.5 / 5.2.14 セキュリティリリース（2026-05-05） | Django セキュリティポリシーに基づく定期リリース。本番稼働中の Django プロジェクトは早めの適用推奨 | [Django Weblog](https://www.djangoproject.com/weblog/2026/may/05/security-releases/) |

## Deep Dive

- [Bun Zig→Rust リライト merge — 経緯と影響](./tu-bun-rust-rewrite.md)
- [Tailwind CSS v4.3 — スクロールバーユーティリティとコンテナサイズクエリ](./tu-tailwind-css-v4-3.md)
