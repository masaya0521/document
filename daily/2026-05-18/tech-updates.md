# Tech Updates — 2026-05-18

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Bun | v1.3.14 リリース | 組み込み画像処理 API `Bun.Image`、`fetch()` の HTTP/2・HTTP/3 クライアント (experimental)、`Bun.serve()` の HTTP/3 (QUIC) を追加。Zig で書かれた最後のバージョン。 | [Bun Blog](https://bun.com/blog/bun-v1.3.14), [GitHub Release](https://github.com/oven-sh/bun/releases/tag/bun-v1.3.14) |
| 2 | PostgreSQL | 18.4 / 17.10 / 16.14 / 15.18 / 14.23 リリース | 11 件のセキュリティ脆弱性と 60 件超のバグを修正。`pg_basebackup`・`pg_rewind` のパストラバーサルや SSL/GSS 再接続による backend クラッシュなどを含む。dump/restore は不要。 | [PostgreSQL News](https://www.postgresql.org/about/news/postgresql-184-1710-1614-1518-and-1423-released-3297/), [Release Notes](https://www.postgresql.org/docs/18/release-18-4.html) |
| 3 | Bun | Zig→Rust リライト PR #30412 マージ | 960,000 行の Zig コードを 6 日間で Rust にポート。Anthropic Claude が大半のコードを生成し、テスト 99.8% パス。canary build で先行利用可能、メモリ安全性が主目的。 | [The Register](https://www.theregister.com/devops/2026/05/14/anthropics-bun-rust-rewrite-merged-at-speed-of-ai/), [HN](https://news.ycombinator.com/item?id=48132488) |
| 4 | Bun | v1.3.13 リリース | `bun test` に `--parallel`・`--isolate`・`--shard`・`--changed` を追加。`bun install` のメモリ使用量が 17 倍削減、`zlib-ng` 採用で gzip が 5.5 倍高速化。82 件の issue を修正。 | [Bun Blog](https://bun.com/blog/bun-v1.3.13) |
| 5 | Python | 3.15 beta 1 / 3.14.4 / 3.13.13 リリース | 3.15 はフィーチャーフリーズ入り。free-threaded CPython の安定 ABI、起動高速化のための lazy imports、ゼロオーバーヘッドのサンプリングプロファイラ、JIT で x86-64 Linux 上 8–9% / Apple Silicon 上 12–13% の改善。 | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/), [The Register](https://www.theregister.com/devops/2026/05/11/feature-freeze-for-python-315-as-first-beta-released/) |
| 6 | .NET / .NET Framework | 2026年5月セキュリティ更新 | CVE-2026-32177 / CVE-2026-35433 の特権昇格を含むセキュリティ・品質改善を提供。.NET 8 / 9 と .NET Framework 4.6.2 以降が対象。 | [.NET Blog](https://devblogs.microsoft.com/dotnet/dotnet-and-dotnet-framework-may-2026-servicing-updates/), [.NET FW Update](https://learn.microsoft.com/en-us/dotnet/framework/release-notes/2026/05-12-may-cumulative-update) |
| 7 | Next.js | 2026年5月セキュリティリリース | 5 月 6–7 日に Next.js と React の脆弱性 13 件を一括修正。middleware/proxy バイパス・XSS・SSRF・キャッシュポイズニング・DoS など。CVE-2026-27979（`maxPostponedStateSize`）と CVE-2026-29057（`http-proxy`）を含む。 | [Vercel Changelog](https://vercel.com/changelog/next-js-may-2026-security-release) |
| 8 | Rust | 1.95.0 リリース | match の if-let guards 安定化、`cfg_select!` マクロ追加（cfg-if 相当）、`str::contains` の aarch64 neon 高速化。stable での custom target spec 受け入れを廃止。 | [Rust Blog](https://blog.rust-lang.org/2026/04/16/Rust-1.95.0/), [LWN](https://lwn.net/Articles/1068011/) |
| 9 | Kubernetes | v1.36 "Haru" リリース | 18 機能が stable へ昇格。HPAScaleToZero がデフォルト ON（HPA でレプリカ 0 までスケール可能に）、SELinux mount option が GA。`gitRepo` ボリュームと IPVS モードの `kube-proxy` を削除。 | [Kubernetes Blog](https://kubernetes.io/blog/2026/04/22/kubernetes-v1-36-release/), [Release Page](https://kubernetes.io/releases/1.36/) |
| 10 | Docker Desktop | Engine v29.3.x 更新 | Kubernetes pod discovery のハング修正、sign-in フロー改善、containerd・Buildx 更新、`Qwen3.5` を Model Runner でサポート。CVE-2026-33990 のセキュリティ修正を含む。 | [Docker Updates](https://releasebot.io/updates/docker) |

## Deep Dive

- [PostgreSQL 18.4 — 11 件の CVE と 60 件超のバグを修正したセキュリティリリース](./tu-postgresql-18-4.md)
- [Bun を 6 日で Zig から Rust へ — AI 駆動の 96 万行ポートが main にマージ](./tu-bun-rust-rewrite.md)
