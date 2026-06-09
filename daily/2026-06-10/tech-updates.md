# Tech Updates — 2026-06-10

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Angular | v22 リリース (6/3) | Signal Forms と Resource API が安定化、OnPush がデフォルトの変更検知戦略に、Incremental Hydration がデフォルト有効化 | [Angular Architects](https://www.angulararchitects.io/en/blog/angular-22-the-most-important-new-features-at-a-glance/), [Ninja Squad](https://blog.ninja-squad.com/2026/06/03/what-is-new-angular-22.0) |
| 2 | PostgreSQL | 19 Beta 1 (6/4) | SQL/PGQ プロパティグラフ、`ON CONFLICT DO SELECT`、`REPACK` コマンド、並列 autovacuum、FK チェック時の INSERT 2倍高速化。GA は 9〜10月予定 | [PostgreSQL News](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/) |
| 3 | Svelte / SvelteKit | June 2026 アップデート | `query.live()` で長寿命リモートクエリ購読（async iterable 対応）、リモートフォームの `submit` がバリデーション結果を boolean で返却、language-tools が TypeScript 6.0 対応 | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-june-2026) |
| 4 | GitHub Copilot (JetBrains) | Copilot CLI 提供開始 (6/2) | JetBrains IDE で Copilot CLI が利用可能に。エージェントピッカー、`/remote` `/compact` `/chronicle` スラッシュコマンド、Agent Debug Panel（public preview） | [GitHub Changelog](https://github.blog/changelog/2026-06-02-introducing-copilot-cli-and-agentic-capabilities-enhancements-in-jetbrains-ides/) |
| 5 | GitHub Copilot (VS Code) | v1.120〜v1.123（5月分） (6/3) | Agents Window が Stable に preview 投入、BYOK（Bring Your Own Key）がエアギャップ環境に拡大、ユーティリティタスク用モデル指定が可能に | [GitHub Changelog](https://github.blog/changelog/2026-06-03-github-copilot-in-visual-studio-code-may-releases/) |
| 6 | Deno | 2.8 / 2.8.2 (5/22, 6/3) | Node.js 互換が 42%→76.4% に大幅向上（Bun を上回る）、バンドル TypeScript を 6.0.3 に更新、cold npm install が 3.66x 高速化 | [Deno Blog](https://deno.com/blog/v2.8), [GitHub Release](https://github.com/denoland/deno/releases/tag/v2.8.2) |
| 7 | Rust | 1.96.0 (5/28) | RFC 3550 の新 range 型（`Iterator` ではなく `IntoIterator` を実装し `Copy` 可能）が標準ライブラリで安定化。サードパーティレジストリ向け CVE 2件を修正 | [Rust Blog](https://blog.rust-lang.org/2026/05/28/Rust-1.96.0/) |
| 8 | Terraform Kubernetes Provider | v3.2.0 (6/4) | HashiCorp 公式の Kubernetes provider のメジャーマイナー更新。Terraform から Kubernetes リソースを操作する標準 provider | [Terraform Registry](https://registry.terraform.io/providers/hashicorp/kubernetes/latest) |
| 9 | PostgreSQL | 18.4 ほか各系列 (5/14) | 18.4 / 17.10 / 16.14 / 15.18 / 14.23 をリリース。11件の CVE と 60件超のバグを修正（CVSS 8.8 の `libpq` スタックオーバーフロー等） | [PostgreSQL News](https://www.postgresql.org/about/news/postgresql-184-1710-1614-1518-and-1423-released-3297/) |
| 10 | TypeScript | 7.0 Beta（Go ネイティブ）(4/21) | コンパイラを Go へ移植した「Project Corsa」のパブリックベータ。`tsgo` 経由で TS 6.0 比 約10倍高速。`@typescript/native-preview@beta` で配布 | [TS Devblog](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/) |

## Deep Dive

- [Angular 22 — Signal Forms / Resource API 安定化と OnPush デフォルト化](./tu-angular-22.md)
- [PostgreSQL 19 Beta 1 — プロパティグラフ・並列 autovacuum・REPACK](./tu-postgresql-19-beta1.md)
