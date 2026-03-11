# Tech Updates — 2026-03-12

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 RC リリース | JS ベース最後のリリース。Go ベースの TS 7.0 への橋渡し。3/17 に GA 予定 | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/) |
| 2 | Rust | 1.94.0 リリース | array_windows、AVX-512 FP16 安定化、Cargo の TOML 1.1 対応、数学定数追加 | [Rust Blog](https://blog.rust-lang.org/2026/03/05/Rust-1.94.0/) |
| 3 | Visual Studio 2026 | GA リリース | AI ネイティブ IDE として登場。C#/C++ エージェント、Profiler/Debugger エージェント搭載 | [Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 4 | Go | 1.26 リリース (2月) | Green Tea GC デフォルト化、cgo オーバーヘッド 30% 削減、crypto/hpke・simd パッケージ追加 | [Go Blog](https://go.dev/blog/go1.26) |
| 5 | GitHub | Dependabot pre-commit 対応 | .pre-commit-config.yaml の rev フィールドを自動更新する PR を作成可能に | [GitHub Changelog](https://github.blog/changelog/2026-03-10-dependabot-now-supports-pre-commit-hooks/) |
| 6 | GitHub | Actions セルフホストランナー課金開始 | 3/1 よりセルフホストランナーに $0.002/分のクラウドプラットフォーム料金を適用 | [GitHub Changelog](https://github.blog/changelog/2025-12-16-coming-soon-simpler-pricing-and-a-better-experience-for-github-actions/) |
| 7 | Redis Cloud | Redis 8.4 提供開始 | Redis Cloud Pro で Redis 8.4 が利用可能に。Redis Enterprise for K8s 7.8.6-13 も公開 | [Redis Changelog](https://redis.io/docs/latest/operate/rc/changelog/march-2026/) |
| 8 | Django | 6.0.2 リリース (2月) | セキュリティ修正・バグ修正を含むメンテナンスリリース | [Django Versions](https://versionlog.com/django/) |
| 9 | GitHub | Secret Scanning パターン更新 | 15 プロバイダーから 28 の新しいシークレット検出器を追加、39 検出器でプッシュ保護をデフォルト有効化 | [GitHub Changelog](https://github.blog/changelog/2026-03-10-secret-scanning-pattern-updates-march-2026/) |
| 10 | Python 3.15 | Alpha 開発中 | UTF-8 デフォルト化、JIT コンパイラ改善、遅延インポート対応。10月 GA 予定 | [PEP 790](https://peps.python.org/pep-0790/) |

## Deep Dive

- [TypeScript 6.0 RC — JS ベース最後のリリースと Go ベース TS 7.0 への道筋](./tu-typescript-6-0.md)
- [Rust 1.94.0 — array_windows、AVX-512 FP16、Cargo TOML 1.1](./tu-rust-1-94.md)
