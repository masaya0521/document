# Tech Updates — 2026-04-26

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Rust | 1.95.0 リリース（2026-04-16） | 新しい `cfg_select!` マクロが安定化。`cfg-if` クレートを置き換える形で条件付きコンパイル分岐を式・文として書けるようになり、`std` の式マクロとして定義済み | [Phoronix](https://www.phoronix.com/news/Rust-1.95-Released), [Rust Changelogs](https://releases.rs/) |
| 2 | pnpm | 11 RC リリース（2026-04-21） | SQLite ベースのストアインデックス、ESM 配布、Node.js v22 以上必須、`minimumReleaseAge=1日` のデフォルト化、ビルドスクリプト設定の `allowBuilds` 統合、グローバルインストール隔離、`pnpm ci` / `pnpm sbom` / `pnpm clean` 等の新コマンド | [InfoQ](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/) |
| 3 | Bun | v1.3.13 リリース（2026-04-20） | `bun test` に `--parallel` / `--isolate` / `--shard` / `--changed`、`bun install` のメモリ消費 17 倍削減、ソースマップのメモリ 8 倍削減、zlib-ng で gzip 5.5 倍高速化、`Bun.serve()` の Range リクエスト対応、SHA3 サポート | [Bun Blog](https://bun.com/blog/bun-v1.3.13) |
| 4 | Python | 3.14.4 リリース（2026-04-07） | 3.14 系 4 番目のメンテナンスリリース。3.14.3 から約 337 件のバグ修正・ビルド改善・ドキュメント変更を含む。3.14 系自体は free-threaded、t-strings、deferred annotation などを搭載 | [Python.org](https://www.python.org/downloads/release/python-3144/) |
| 5 | PostgreSQL | 19 feature freeze（2026-04-08 12:00 UTC） | メジャーバージョン 19 の機能凍結が開始。今後はバグ修正と安定化に集中し、5 月から beta 開始予定。GA は 2026-09 を予定。期待される機能はパーティショニング改善・論理レプリケーション拡張・ベクター検索の足場固めなど | [pgsql-hackers](https://www.postgresql.org/message-id/ab1YPhD9XNwQH7Kn@nathan), [PG 19 ドラフト](https://www.postgresql.org/docs/devel/release-19.html) |
| 6 | SQLite | 3.53.0 リリース（2026-04-09） | 通常のメンテナンス・改善リリース。クエリプランナー・bytecode 改良などを継続的に積み上げ、組み込み DB の事実上のデファクトとしての地位を保つ | [VersionLog](https://versionlog.com/sqlite/) |
| 7 | Docker | Docker Sandboxes 公開（2026-04-16） | microVM ベースで強力なエージェント分離を提供する新機能。AI/エージェントが実行する任意コードを安全にサンドボックス化することを目的とし、ローカル開発機の保護を強化 | [Docker Blog](https://www.docker.com/blog/docker-terraform-provider/) |
| 8 | GitHub Actions | Early April 2026 アップデート（2026-04-02） | サービスコンテナで `entrypoint` / `command` のオーバーライドが可能に（Docker Compose 互換構文）、OIDC のレポジトリ Custom Properties クレームが GA、Azure VNET 経由ホストランナーのフェイルオーバーが Public Preview | [GitHub Changelog](https://github.blog/changelog/2026-04-02-github-actions-early-april-2026-updates/) |
| 9 | GitHub Copilot CLI | カスタム MCP レジストリ allowlist 対応（2026-04-16） | エンタープライズ／組織管理者が独自の MCP レジストリを持ち込み、Copilot CLI で許可ポリシーを強制できるようになった。エージェントが利用するツールセットを組織で統制可能に | [GitHub Changelog](https://github.blog/changelog/2026-04-16-copilot-cli-supports-custom-registry-based-mcp-allowlists/) |
| 10 | GitHub | Global Pull Requests Dashboard が opt-out Public Preview に（2026-04-23） | 新しい統合 PR ダッシュボードが全ユーザーにデフォルト適用。ダッシュボードと Inbox の切替、組織別フィルタ、Drafts／Waiting for review 区分、チームレビュー、未読インジケーター、ステータスチェック表示、担当者アバターなどを搭載 | [GitHub Changelog](https://github.blog/changelog/2026-04-23-global-pull-requests-dashboard-moves-to-opt-out-public-preview/) |

## Deep Dive

- [pnpm 11 RC — SQLite ストアと供給網セキュリティの強化](./tu-pnpm-11-rc.md)
- [Rust 1.95 — `cfg_select!` マクロで条件付きコンパイルを式に](./tu-rust-1-95.md)
