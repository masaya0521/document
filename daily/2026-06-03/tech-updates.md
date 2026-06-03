# Tech Updates — 2026-06-03

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Angular | v22 GA（2026-06-03 週リリース） | Signal Forms 安定化、selectorless components、zoneless / OnPush デフォルト化など「Signal-First」時代を確立するメジャーリリース | [Releases](https://github.com/angular/angular/releases), [angular.dev](https://angular.dev/reference/releases) |
| 2 | Python | 3.15.0b2 リリース（2026-06-02） | 3.15 系の 2 度目のベータ。10月の正式リリースに向けた機能フリーズ直前の検証版。あわせて 3.14.4 系の保守版も継続中 | [Python Insider](https://blog.python.org/), [PEP 790](https://peps.python.org/pep-0790/) |
| 3 | Deno | 2.8 リリース（2026-05-22） | `import defer` 対応、6 つの新サブコマンド（transpile / pack / bump-version / ci / why / audit fix）、Chrome DevTools ネットワーク統合、cold npm install 3.66 倍高速化 | [Deno Blog](https://deno.com/blog/v2.8) |
| 4 | VS Code | 1.122 リリース（2026-05-28） | Anthropic / OpenAI モデルで 1M コンテキスト対応、サインイン不要の air-gapped BYOK、統合ブラウザのデバイスエミュレーション | [Release Notes](https://code.visualstudio.com/updates/v1_122) |
| 5 | Ruby | 4.0.5 リリース（2026-05-20） | Ruby 4.0 系の安定保守リリース。バグ修正・セキュリティ修正を含む | [Ruby Releases](https://www.ruby-lang.org/en/downloads/releases/), [GitHub](https://github.com/ruby/ruby/releases) |
| 6 | PostgreSQL | 18.4 / 17.10 / 16.14 / 15.18 / 14.23（2026-05-14） | 11 件の脆弱性と 60 件超のバグ修正を含む四半期定例セキュリティリリース。tzdata 2026b へ更新 | [News](https://www.postgresql.org/about/news/postgresql-184-1710-1614-1518-and-1423-released-3297/) |
| 7 | Kubernetes | v1.36「Haru」（2026-05-13） | 70 の機能強化（Stable 18 / Beta 25 / Alpha 25）。Workload API と PodGroup API による workload-aware scheduling を導入 | [Blog](https://kubernetes.io/blog/2026/05/13/kubernetes-v1-36-advancing-workload-aware-scheduling/) |
| 8 | Docker | Docker Engine 29 / Desktop（2026-05） | Logs view の GA、Model Runner の OpenAI Responses API 対応。Linux 版で RHEL 8 サポート終了 | [Engine 29 Notes](https://docs.docker.com/engine/release-notes/29/), [Desktop Notes](https://docs.docker.com/desktop/release-notes/) |
| 9 | Tailwind CSS | 4.3.0 リリース（2026-05） | v4 系の最新マイナー。4.2 が 2026-05-08 に EOL。Oxide エンジン世代の継続改善 | [VersionLog](https://versionlog.com/tailwind-css/) |
| 10 | Astro | 6.4 リリース（Sätteri） | Rust 製の高速 Markdown / MDX パイプライン「Sätteri」を `@astrojs/markdown-satteri` として導入。大規模ドキュサイトのビルドを 1 分以上短縮 | [Astro Blog](https://astro.build/blog/astro-640/) |

## Deep Dive

- [Angular 22 — Signal-First 時代の到来](./tu-angular-22.md)
- [Deno 2.8 — import defer と 6 つの新サブコマンド](./tu-deno-2-8.md)
