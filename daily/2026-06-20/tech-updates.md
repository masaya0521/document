# Tech Updates — 2026-06-20

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | VS Code | v1.125（6/17） | 統合ブラウザの強化、Marketplace 経由の追加モデルインストール、拡張機能の自動更新タイミング制御、Copilot のエンタープライズ向けポリシー管理（Windows/macOS のデバイス管理経由で設定配布）を追加 | [Release Notes](https://code.visualstudio.com/updates/v1_125) |
| 2 | GitHub CLI | `gh repo read-file` / `gh repo read-dir`（6/17） | リポジトリをクローンせずにファイル内容・ディレクトリ構成を読み取れる新コマンドを追加。CI や軽量スクリプトでの利用に有用 | [GitHub Changelog](https://github.blog/changelog/month/06-2026/) |
| 3 | GitHub Copilot / Actions | コードレビュー強化・PR セキュリティ既定強化（6/18） | Copilot コードレビューが `AGENTS.md` 対応とドラフト PR でのレビュー依頼に対応。GitHub Actions は `pull_request_target` でより安全なデフォルト設定を実装、重複 Issue 検出も Public Preview 開始 | [GitHub Changelog](https://github.blog/changelog/month/06-2026/) |
| 4 | Angular | v22（6/3） | OnPush がデフォルトの変更検出戦略に（破壊的変更）。Signal Forms・Resource API・Zoneless が本番対応。`@Service` デコレータや `injectAsync`、`debounced()` Signal を追加 | [DEV: Angular 22](https://dev.to/rigole/angular-22-is-here-everything-you-need-to-know-4g3c) |
| 5 | Astro | v6.4（5/28） | Rust 製 Markdown プロセッサ「Sätteri」を新パッケージ `@astrojs/markdown-satteri` として導入。プラガブルな `markdown.processor` API でビルド時間を大幅短縮（公式ドキュメントサイトで 1 分以上短縮） | [Astro Blog](https://astro.build/blog/astro-640/) |
| 6 | Tailwind CSS | v4.3.1（6月） | `@tailwindcss/cli` に `--silent` オプション追加。Node 26 以上での非推奨警告除去、`@apply` の CSS ミキシン対応、`not-*` のコンテナクエリ否定修正など | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases) |
| 7 | Next.js | v16.2.7（6月） | 16.2 系の安定版パッチリリース。継続的なバグ修正と安定化 | [GitHub Releases](https://github.com/vercel/next.js/releases) |
| 8 | Python | 3.15 フィーチャーフリーズ（6/9） | Python 3.15 が機能凍結（beta 段階）に到達。最終リリースは 2026 年 10 月予定。3.15 に入る機能が確定 | [Real Python](https://realpython.com/python-news-june-2026/), [PEP 790](https://peps.python.org/pep-0790/) |
| 9 | Rust | v1.96.0（5/28） | Copy を実装する新しい Range 型群（RFC3550）、パターンマッチを伴う assert、Wasm の未定義シンボルをハードリンクエラー化、Cargo の脆弱性 2 件（CVE-2026-5222/5223）を修正 | [Rust Blog](https://blog.rust-lang.org/2026/05/28/Rust-1.96.0/) |
| 10 | Terraform Kubernetes Provider | v3.2.0（6/4） | HashiCorp 公式 Kubernetes プロバイダのマイナーリリース | [Terraform Registry](https://registry.terraform.io/providers/hashicorp/kubernetes/latest) |

## Deep Dive

- [Angular 22 — OnPush デフォルト化と Signal Forms 本番対応](./tu-angular-22.md)
- [Astro 6.4 — Rust 製 Markdown プロセッサ Sätteri](./tu-astro-6-4-satteri.md)
