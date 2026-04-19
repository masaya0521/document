# Tech Updates — 2026-04-20

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Node.js | 24.15.0 LTS リリース (2026-04-15) | Explicit Resource Management (`using`/`await using`) を V8 13.6 で正式搭載。Undici 7 による HTTP クライアント改善。MSVC サポート廃止で ClangCL 必須に | [versionlog](https://versionlog.com/nodejs/24/), [CHANGELOG_V24](https://github.com/nodejs/node/blob/main/doc/changelogs/CHANGELOG_V24.md) |
| 2 | Visual Studio Code | 1.116 リリース (2026-04-15) | GitHub Copilot Chat が組み込み拡張に昇格（追加インストール不要）。Agent デバッグログ、ターミナル Agent ツール、Copilot CLI の thinking effort 設定を追加 | [VS Code 1.116](https://code.visualstudio.com/updates/v1_116) |
| 3 | Python | 3.14.4 / 3.15.0a8 / 3.13.13 リリース (2026-04-07) | 3.14 系の 4 回目のメンテナンスリリース。約 337 件のバグ修正。併せて 3.15 alpha8 と 3.13 セキュリティアップデートも配信 | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/), [Release page](https://www.python.org/downloads/release/python-3144/) |
| 4 | Deno | 2.6 系メンテナンスリリース (2026-04-09) | `MIMEType`, `convertProcessSignalToExitCode`, ChildProcess の `Symbol.dispose` 追加。Windows での追加シグナル対応、OTEL 属性の配列値サポート、`--cpu-prof-flamegraph` フラグで SVG フレームグラフ出力 | [Deno Releases](https://github.com/denoland/deno/releases) |
| 5 | Bun | v1.3.11 / v1.3.12 リリース (2026-04-09) | 105 件の issue 修正。v1.3 系のメンテナンスラインが継続的に進行中 | [Bun Releases](https://github.com/oven-sh/bun/releases) |
| 6 | Vite | 8.0.4 → 8.0.8 (2026-04-06 〜 04-09) | esbuild 0.28 を peer dep として許容。HMR の更新ファイル一覧を truncate、依存スキャンの所要時間を 1 秒超で報告。Rolldown を 1.0.0-rc.15 に更新 | [Vite 8 Blog](https://vite.dev/blog/announcing-vite8), [CHANGELOG](https://github.com/vitejs/vite/blob/main/packages/vite/CHANGELOG.md) |
| 7 | JetBrains IDEs | 2026.1 シリーズリリース (2026-04-09) | PhpStorm 2026.1 が MCP ツール対応・Git worktree サポートを追加。Rider / ReSharper Ultimate / CLion 等もメジャー更新 | [JetBrains Blog](https://blog.jetbrains.com/category/releases/), [CLion 2026.1](https://blog.jetbrains.com/clion/2026/03/2026-1-release/) |
| 8 | Docker Desktop | 2026 年 4 月アップデート | WSL 2 起動時間短縮、MCP Toolkit でプロファイル/カスタムカタログ機能追加、vLLM Metal サポート。CVE-2026-33990 (SSRF)、CVE-2026-2664 (OOB read)、CVE-2026-28400 を修正 | [Docker Desktop Release Notes](https://docs.docker.com/desktop/release-notes/) |
| 9 | PostgreSQL 19 | Feature Freeze 開始 (2026-04-08) | PostgreSQL 19 の feature freeze が正式に発動。新規機能のマージを停止し、5 月以降の beta 1 に向けて安定化フェーズへ移行。正式リリースは 2026-09 予定 | [versionlog PG 19](https://versionlog.com/blog/postgresql-19-whats-coming-september-2026/) |
| 10 | Redis Enterprise for Kubernetes | 7.8.6-14 リリース (2026-04) | Redis Software 7.8.6-260 をサポートするメンテナンスリリース。K8s 上での Redis 運用の安定性向上 | [RedisLabs K8s Releases](https://github.com/RedisLabs/redis-enterprise-k8s-docs/releases) |

## Deep Dive

- [Node.js 24.15.0 LTS — Explicit Resource Management と ClangCL 必須化](./tu-node-24-15-lts.md)
- [VS Code 1.116 — Copilot 同梱と Agent 開発環境の刷新](./tu-vscode-1-116.md)
