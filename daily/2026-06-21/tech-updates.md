# Tech Updates — 2026-06-21

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Node.js | v24.17.0 / v26.3.1（セキュリティリリース） | 6/17〜18 に複数の脆弱性（最高 HIGH）に対応する緊急セキュリティリリース。全アクティブラインで配布、早期アップデート推奨 | [Node.js Blog](https://nodejs.org/en/blog/vulnerability/june-2026-security-releases) |
| 2 | Visual Studio Code | v1.125 | 6/17 リリース。統合ブラウザのアドレスバー検索・リモート越しセキュア接続、Model Provider のインストール導線、拡張機能の自動更新遅延設定、MDM 経由の Copilot 設定配布、LSP 3.18 対応 | [Release Notes](https://code.visualstudio.com/updates/v1_125) |
| 3 | Svelte / SvelteKit | Svelte 5.56.0 / SvelteKit 2.61.0 | Remote Functions が大幅刷新。`query.live()` の async-iterable 化、イベントハンドラ/モジュールスコープでの query await 対応。**破壊的変更**: `.run()` 廃止、enhance コールバックの引数変更 | [What's new in Svelte](https://svelte.dev/blog/whats-new-in-svelte-june-2026) |
| 4 | Python | 3.14.6 / 3.13.14 | 6/10 リリース。両系列のバグfix・セキュリティメンテナンスリリース | [Python downloads](https://www.python.org/downloads/) |
| 5 | Go | 1.25.11 / 1.26.4 | 6/2 リリース。`crypto/x509`・`mime`・`net/textproto` のセキュリティfix、コンパイラ/ランタイムのバグfix | [Go Release History](https://go.dev/doc/devel/release) |
| 6 | .NET | 10.0.9 / 9.0.17 / 8.0.28 | 6/9 サービシングリリース。3 件の CVE（CVE-2026-45591/45491/45490）を含むセキュリティ・非セキュリティfix | [.NET Blog](https://devblogs.microsoft.com/dotnet/dotnet-and-dotnet-framework-june-2026-servicing-updates/) |
| 7 | Visual Studio 2026 | 6 月アップデート | 6/9 リリース。OS のライト/ダーク設定に追従する自動テーマ切替、Fluent カラートークンを IDE 内で直接カスタマイズできる Theme colors 設定ページを追加 | [Release Notes](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 8 | WordPress (Gutenberg) | 23.3 / 23.2 | 6 月リリース。新ウィジェット 5 種（Site Health, News, Events, Quick Draft 等）、サイトプレビュー/URL バー、コンテナブレークポイント対応のグリッドカラムなどエディタ強化 | [WordPress Dev News](https://developer.wordpress.org/news/2026/06/whats-new-for-developers-june-2026/) |
| 9 | Supabase | Passkeys（WebAuthn） | 6 月の Developer Update。Face ID / Touch ID / Windows Hello・デバイス PIN・ハードウェアキーでのサインインに対応。WebAuthn 準拠でフィッシング耐性のあるパスワードレス認証を提供 | [Supabase Changelog](https://supabase.com/changelog/46689-developer-update-june-2026) |
| 10 | Terraform Kubernetes Provider | hashicorp/kubernetes v3.2.0 | 6/4 公開。公式 Kubernetes プロバイダのメジャーマイナー更新 | [Terraform Registry](https://registry.terraform.io/providers/hashicorp/kubernetes/latest) |

## Deep Dive

- [Visual Studio Code 1.125 — 統合ブラウザと Model Provider 導線の強化](./tu-vscode-1-125.md)
- [Svelte / SvelteKit June 2026 — Remote Functions の刷新と破壊的変更](./tu-svelte-june-2026.md)
