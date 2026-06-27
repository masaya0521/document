# Tech Updates — 2026-06-28

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Deno | v2.9 リリース（6/25） | `deno desktop` でWeb技術によるネイティブデスクトップアプリ開発が可能に。npm/pnpm/yarn/Bun のロックファイルからの移行対応、CSS モジュールインポート、Node.js 26 互換 | [Deno Blog](https://deno.com/blog/v2.9) |
| 2 | Next.js | v16.3 Preview 公開（6/26） | Instant Navigations による SPA ライクな高速遷移、`AGENTS.md` 同梱、agent browser での React introspection、actionable errors | [Next.js Blog](https://nextjs.org/blog/next-16-3-instant-navigations) |
| 3 | Node.js | v24.17.0 / v26.3.1 セキュリティリリース（6/18） | High 2件を含む12脆弱性を修正。WebCrypto AES 整数オーバーフロー（CVE-2026-48933）、TLS ホスト名検証バイパス（CVE-2026-48618）等 | [Node.js Security](https://nodejs.org/en/blog/vulnerability/june-2026-security-releases) |
| 4 | VS Code | v1.126 リリース（6/24） | セッション単位のコスト表示、1セッション内での複数チャット並行実行、未知フォルダを安全に閲覧する Workspace Trust（restricted mode） | [VS Code Updates](https://code.visualstudio.com/updates/v1_126) |
| 5 | Vite | v8.1 リリース（6/23） | 実験的な Bundled Dev Mode で大規模アプリの起動が最大15倍高速化。Wasm ESM 統合、`import.meta.glob` の caseSensitive オプション追加 | [Vite Blog](https://vite.dev/blog/announcing-vite8-1) |
| 6 | Angular | v22 リリース（6/3、v22.0.2 が 6/17） | "signal-first" 時代へ。Signal Forms / Resource API が安定化、`OnPush` がデフォルトの変更検知戦略に、`@Service` / `injectAsync` / `debounced` 追加 | [Angular Blog](https://blog.angular.dev/announcing-angular-v22-c52bb83a4664) |
| 7 | Tailwind CSS | v4.3 リリース（6/12） | ファーストパーティの scrollbar ユーティリティ（幅・色・gutter 制御）、`zoom-*` / `tab-*`、stacked & compound `@variant` サポート、機能ユーティリティのデフォルト値 | [Tailwind Blog](https://tailwindcss.com/blog) |
| 8 | Python | v3.14.6 リリース（6/10） | 3.14 系のメンテナンスリリース。バグ修正・セキュリティ修正を含む | [Python Downloads](https://www.python.org/downloads/source/) |
| 9 | Go | v1.26.4 / v1.25.11 リリース（6/2） | 両アクティブブランチのパッチリリース。1.26 はデフォルト有効化された Green Tea GC、`new` の式引数対応が目玉 | [Go Release History](https://go.dev/doc/devel/release) |
| 10 | Terraform | 2026年6月アップデート | `terraform init` のクラッシュ修正、null に評価される module version のサポート、Linux s390x（zLinux）ビルド追加 | [Terraform Releases](https://releases.sh/hashicorp/terraform) |

## Deep Dive

- [Angular 22 — signal-first 時代への移行](./tu-angular-22.md)
- [Deno 2.9 — deno desktop とエコシステム移行の強化](./tu-deno-2-9.md)
