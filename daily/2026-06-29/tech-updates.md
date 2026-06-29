# Tech Updates — 2026-06-29

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Deno | v2.9 リリース（6/25） | `deno desktop` でWeb技術からネイティブデスクトップアプリを構築可能に。npm/pnpm/yarn/Bun からのファーストクラス移行、CSS module imports、スナップショット/パラメータ化テスト、`deno compile --bundle` のバイナリ縮小、Node.js 26 互換を追加 | [Deno Blog](https://deno.com/blog?tag=product-update) |
| 2 | Angular | v22 リリース（6/3） | 「signal-first」時代の本格化。Selectorless components（セレクタ文字列なしでテンプレートに直接 import 可能）を導入。Active support は 2026/12 まで、LTS は 2028/5 まで | [Angular Releases](https://github.com/angular/angular/releases) |
| 3 | VS Code | v1.126 リリース（6/24） | コスト透明性の向上、モデルチューニングの簡素化、未知のコードをより安全に閲覧する機能を追加。エージェントと統合ブラウザの操作性も継続改善 | [Release Notes](https://code.visualstudio.com/updates/v1_126) |
| 4 | Next.js | v16.3 Preview | Instant navigations と partial prefetching による SPA ライクな高速ルート遷移。AI 向けドキュメントバンドル・Skills・ブラウザ introspection・actionable errors も追加（安定版は 16.2.7） | [Next.js Updates](https://releasebot.io/updates/vercel/next-js) |
| 5 | PostgreSQL | v19 Beta 1（6/4） | 次期メジャー PostgreSQL 19 の最初のベータが公開。安定版の最新は 18.4（5/11） | [PostgreSQL](https://versionlog.com/postgresql/) |
| 6 | Python | v3.14.6（6/10） | 3.14 系の 6 回目のメンテナンスリリース。約 179 件のバグ修正・ビルド改善・ドキュメント更新。同時に 3.13.14 もリリース。3.15 は 6 月にフィーチャーフリーズ | [Python Insider](https://blog.python.org/2026/06/python-3146-31314.html) |
| 7 | Go | v1.26.4 / v1.25.11（6/2） | crypto/x509・mime・net/textproto のセキュリティ修正に加え、コンパイラ・ランタイム・`go fix`・crypto/fips140 のバグ修正を含むポイントリリース | [Go Release History](https://go.dev/doc/devel/release) |
| 8 | MySQL | v9.7.1 / v8.4.10（6/3） | Innovation 系（9.7.1）と LTS 系（8.4.10）の同時パッチリリース | [MySQL Version History](https://versionlog.com/mysql/) |
| 9 | Terraform Kubernetes Provider | v3.2.0（6/4） | HashiCorp 公式 Kubernetes プロバイダのメジャー系最新版。Kubernetes リソース管理機能を拡充 | [Terraform Registry](https://registry.terraform.io/providers/hashicorp/kubernetes/latest) |
| 10 | Astro | v6.4.4 | Astro 6 系の最新安定版。引き続きデフォルトでゼロ JavaScript 配信を志向 | [Astro Releases](https://github.com/withastro/astro/releases) |

## Deep Dive

- [Deno 2.9 — deno desktop とパッケージマネージャ移行](./tu-deno-2-9.md)
- [Angular 22 — signal-first と Selectorless Components](./tu-angular-22.md)
