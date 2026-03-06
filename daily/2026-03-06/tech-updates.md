# Tech Updates — 2026-03-06

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 RC リリース、3/17 に安定版予定 | JavaScript ベース最後のメジャーリリース。7.0 では Go ベースコンパイラに移行予定。5〜10倍のコンパイル高速化への橋渡し | [GitHub](https://github.com/microsoft/typescript/releases), [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/) |
| 2 | Deno | 2.7.2 リリース | V8 14.6 搭載、Temporal API の安定化、Windows ARM ビルド対応、npm overrides サポート、require(esm) 修正 | [GitHub](https://github.com/denoland/deno/releases/tag/v2.7.2), [公式ブログ](https://deno.com/blog/v2.7) |
| 3 | Go | 1.26 リリース（2月） | Green Tea GC がデフォルト有効化（GC オーバーヘッド 10〜40% 削減）、go fix の刷新、goroutineleak プロファイル、SIMD パッケージ追加 | [公式](https://go.dev/blog/go1.26), [リリースノート](https://go.dev/doc/go1.26) |
| 4 | Python | 3.12.13 / 3.11.15 / 3.10.20 セキュリティリリース | 3月3日に旧バージョン系列のセキュリティバグフィックスリリースを一斉公開 | [Python.org](https://www.python.org/downloads/release/python-31213/) |
| 5 | Python | 3.15.0 alpha 7（3/10 予定） | 新しい統計サンプリングプロファイラ（PEP 799）、内包表記でのアンパック（PEP 798）、UTF-8 デフォルトエンコーディング（PEP 686） | [PEP 790](https://peps.python.org/pep-0790/), [Python Insider](https://pythoninsider.blogspot.com/2026/02/python-3150-alpha-6.html) |
| 6 | Rust | 1.94.0 Beta（3/5） | 6週間サイクルで新ベータ版がリリース。現在の安定版は 1.93.1（2/12 リリース） | [公式](https://blog.rust-lang.org/releases/), [リリースノート](https://blog.rust-lang.org/2026/02/12/Rust-1.93.1/) |
| 7 | Docker | Hardened System Packages 発表 | マルチディストロ対応のセキュア・バイ・デフォルトコンポーネント。CVE ほぼゼロを実現。Engine 29.2.1 が最新安定版 | [Docker](https://www.docker.com/blog/docker-terraform-provider/), [リリースノート](https://docs.docker.com/desktop/release-notes/) |
| 8 | Rails | 8.1 リリース | Active Job Continuations（長時間ジョブのチェックポイント再開）、ネイティブ Markdown レンダリング、Local CI DSL。500+ コントリビュータによる 2,500 コミット | [公式](https://rubyonrails.org/category/releases) |
| 9 | Astro | 6 Beta | Cloudflare による買収後初のメジャーリリース候補。Vite Environment API と Workerd dev server 統合による開発パフォーマンス向上 | [Criztec](https://criztec.com/astro-6-beta-and-next-js-16-the-87xw/) |
| 10 | JetBrains | CodeCanvas 3/31 終了 | クラウド開発環境 CodeCanvas のサービス終了を発表。Fleet に続く開発環境の整理統合 | [Neowin](https://www.neowin.net/news/jetbrains-retires-codecanvas-will-be-unusuable-on-march-31-2026/) |

## Deep Dive

- [TypeScript 6.0 — JavaScript ベース最後のメジャーリリース](./tu-typescript-6.md)
- [Go 1.26 — Green Tea GC と開発者体験の進化](./tu-go-1-26.md)
