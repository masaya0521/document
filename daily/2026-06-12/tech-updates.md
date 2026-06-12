# Tech Updates — 2026-06-12

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | PostgreSQL | 19 Beta 1（6/4） | SQL/PGQ プロパティグラフクエリ、`REPACK` コマンド、並列 autovacuum、`ON CONFLICT DO SELECT` 等。JIT デフォルト無効化・デフォルト圧縮 lz4 化などの破壊的変更あり | [公式アナウンス](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/) |
| 2 | Python | 3.15.0 Beta 2（6/2） | feature freeze 後 2 度目のベータ。明示的 lazy imports（PEP 810）、`frozendict`（PEP 814）、JIT 改善（x86-64 Linux で 8-9% 高速化）等 | [python.org](https://www.python.org/downloads/release/python-3150b2/) |
| 3 | Visual Studio | 2026 GA（6/9） | メジャーリリース。AI のプラットフォーム深層統合、起動・ビルドのパフォーマンス改善、TypeScript 7 native preview 統合 | [リリースノート](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 4 | VS Code | 1.124（6/10） | Advanced Autopilot がデフォルト有効化（最大 3 ループ）、バックグラウンドセッション送信（Alt+Enter）、セッションピッカー（Ctrl+R）、統合ブラウザ履歴 | [リリースノート](https://code.visualstudio.com/updates/v1_124) |
| 5 | Go | 1.26.4 / 1.25.9（6/2） | セキュリティリリース。`crypto/x509`・`mime`・`net/textproto` の脆弱性修正、コンパイラ・ランタイムのバグ修正 | [golang-announce](https://groups.google.com/g/golang-announce/c/0uYbvbPZRWU) |
| 6 | .NET | 10.0.9 / 9.0.17 / 8.0.28（6/9） | 6 月のサービシングリリース。CVE-2026-45491・CVE-2026-45490 の 2 件のセキュリティ修正を含む | [.NET Blog](https://devblogs.microsoft.com/dotnet/dotnet-and-dotnet-framework-june-2026-servicing-updates/) |
| 7 | Rust | 1.96.0（5/28） | RFC 3550 の Copy 対応新 Range 型（`core::range`）、新アサーションマクロ安定化、Cargo の CVE-2026-5223 / CVE-2026-5222 修正 | [Rust Blog](https://blog.rust-lang.org/2026/05/28/Rust-1.96.0/) |
| 8 | Node.js | 26.3.0（Current） | 5 月に Current 化した 26 系の最新マイナー。26 系は 2026-10-28 に LTS 昇格予定。6/17 に 26.x / 24.x / 22.x のセキュリティリリースが予告されている | [nodejs.org](https://nodejs.org/en/about/previous-releases), [セキュリティ予告](https://nodejs.org/en/blog/vulnerability/june-2026-security-releases) |
| 9 | GitHub CLI | issue types / sub-issues 対応 | `gh` コマンドから issue type・親子 issue（sub-issue）・issue 依存関係を直接操作可能に。`gh api` の生スクリプトが不要になった | [GitHub Changelog](https://releasebot.io/updates/github) |
| 10 | WordPress | Gutenberg 23.3 | メディアエディタモーダルがデフォルトのクロップ体験に。フリーフォーム / アスペクト比クロップ、回転・ズーム・メタデータ編集を統合 | [WordPress Developer Blog](https://developer.wordpress.org/news/2026/06/whats-new-for-developers-june-2026/) |

## Deep Dive

- [PostgreSQL 19 Beta 1 — SQL/PGQ・REPACK・並列 autovacuum と破壊的変更](./tu-postgresql-19-beta1.md)
- [Python 3.15 Beta — lazy imports・frozendict・JIT 改善](./tu-python-3-15-beta.md)
