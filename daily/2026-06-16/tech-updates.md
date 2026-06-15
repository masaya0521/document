# Tech Updates — 2026-06-16

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Angular | v22.0 リリース（6/3） | Signal Forms / Resources が安定化、`OnPush` がデフォルトの変更検知戦略に、HttpClient が Fetch API デフォルトに。signal-first 時代へ本格移行 | [Ninja Squad](https://blog.ninja-squad.com/2026/06/03/what-is-new-angular-22.0), [angular.love](https://angular.love/angular-22-key-features-and-changes) |
| 2 | Astro | v6.4 リリース（6/4） | Rust 製の新 Markdown/MDX パイプライン「Sätteri」(`@astrojs/markdown-satteri`) を導入。大規模ドキュメントのビルドが1分以上短縮。`markdown.processor` で処理系を差し替え可能に | [Astro Blog](https://astro.build/blog/astro-640/) |
| 3 | PostgreSQL | 19 Beta 1 リリース（6/4） | パラレル autovacuum、`REPACK`（非ブロッキングなテーブル再編成）、SQL/PGQ プロパティグラフクエリ、`FOR PORTION OF` 時相操作など 200 超の変更。GA は 2026 年秋頃 | [PostgreSQL News](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/) |
| 4 | Django | 6.0.6 リリース（6/3） | 6.0 系のバグフィックスリリース。Python 3.14 の遅延アノテーション関数の検査不具合などを修正 | [PyPI](https://pypi.org/project/Django/), [Django Releases](https://docs.djangoproject.com/en/6.0/releases/) |
| 5 | Go | 1.26.4 / 1.25.10 セキュリティリリース（6/2） | `crypto/x509`・`mime`・`net/textproto` のセキュリティ修正に加え、コンパイラ・ランタイム・`go fix`・`crypto/fips140` のバグ修正 | [golang-announce](https://groups.google.com/g/golang-announce/c/qcCIEXso47M), [Go Release History](https://go.dev/doc/devel/release) |
| 6 | .NET | June 2026 サービシング更新（6/9） | .NET 10.0.9 / 9.0.17 / 8.0.28 をリリース。3 件の CVE（CVE-2026-45591 / 45491 / 45490）を修正。.NET Framework は今月更新なし | [.NET Blog](https://devblogs.microsoft.com/dotnet/dotnet-and-dotnet-framework-june-2026-servicing-updates/) |
| 7 | VS Code | 1.124 リリース（6/10） | Agents ウィンドウのバックグラウンド送信・キーボードナビゲーション強化、Autopilot がデフォルト有効化、ブラウザ履歴トラッキングなど | [VS Code Updates](https://code.visualstudio.com/updates/v1_124) |
| 8 | Node.js | セキュリティリリース告知（6/17 予定） | 24.x 系を含む複数リリースラインで HIGH severity の脆弱性修正を予告。事前告知のうえ 6/17 にリリース予定 | [Node.js Security](https://nodejs.org/en/blog/vulnerability/june-2026-security-releases) |
| 9 | Google Kubernetes Engine | 1.35.5-gke.1241000 リリース（6/12） | GKE の最新マイナーアップデート。1.33 は 6/28 に EOL を迎えるため移行が必要 | [GKE Release Notes](https://docs.cloud.google.com/kubernetes-engine/docs/release-notes) |
| 10 | TypeScript | 7.0 Beta（5/31、ウォッチ継続） | Go ベースのネイティブコンパイラ。6.0 比で「しばしば約 10 倍高速」を謳う。RC は数週間以内、正式版は夏頃を予定。当面の最大トピックとして注目 | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/) |

## Deep Dive

- [Angular 22 — signal-first 時代の本格到来](./tu-angular-22.md)
- [PostgreSQL 19 Beta 1 — パラレル autovacuum と REPACK、プロパティグラフ](./tu-postgresql-19-beta.md)

---

> ℹ️ 6/16 時点で当週はメジャーリリースが集中した週ではなかったため、6 月初旬〜中旬の主要リリースを横断的に採録しています。フロントエンド（Angular / Astro）、バックエンド・言語（Django / Go / .NET）、DB（PostgreSQL）、ランタイム（Node.js）、開発ツール（VS Code）、インフラ（GKE）を網羅。
