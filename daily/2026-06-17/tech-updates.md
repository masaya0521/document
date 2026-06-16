# Tech Updates — 2026-06-17

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | VS Code | v1.124 リリース（6/10） | Agents ウィンドウ（バックグラウンドセッション・履歴ナビゲーション）、Autopilot のデフォルト有効化、統合ブラウザの履歴機能を追加 | [Release Notes](https://code.visualstudio.com/updates/v1_124) |
| 2 | Python | 3.14.6 リリース（6/10） | 3.14 系の最新安定版パッチ。tail-call インタプリタ・遅延アノテーション評価・free-threading の改善を含む 3.14 系の継続メンテナンスリリース | [Python Releases](https://versionlog.com/python/) |
| 3 | GitHub Copilot SDK | GA（6/2） | Copilot の agentic engine を自前アプリに組込可能に。Rust / Java を新規追加し計6言語対応、カスタムツール・MCP・OpenTelemetry をサポート | [GitHub Changelog](https://github.blog/changelog/2026-06-02-copilot-sdk-is-now-generally-available/) |
| 4 | GitHub Copilot Code Review | 新設定・制御（6/12） | 組織ランナー制御、コンテンツ除外サポート、リポジトリカスタム instruction の文字数制限撤廃を追加 | [GitHub Changelog](https://github.blog/changelog/2026-06-12-copilot-code-review-new-configurations-and-controls/) |
| 5 | GitHub Copilot CLI | `/security-review` コマンド（6/10） | 本番前にセキュリティ脆弱性を検出する実験的スラッシュコマンドを public preview で提供開始 | [GitHub Changelog](https://github.blog/changelog/2026-06-10-dedicated-security-review-command-now-available-in-copilot-cli/) |
| 6 | Terraform Kubernetes Provider | v3.2.0 リリース（6/4） | HashiCorp 公式 Kubernetes プロバイダのアップデート | [Terraform Registry](https://registry.terraform.io/providers/hashicorp/kubernetes/latest) |
| 7 | Supabase | ChatGPT 連携追加（6月） | プロジェクトを ChatGPT に接続する連携を追加。SQL 実行・スキーマ変更・ブランチ・Edge Function デプロイ・ライブログなど29ツールをカバー | [Supabase Changelog](https://supabase.com/changelog/46689-developer-update-june-2026) |
| 8 | MSVC Build Tools | Preview 更新（6月） | x86 の16bitオーバーフロー intrinsic の codegen バグ修正、インライナーの戻り値コスト分析追加、関数ポインタの devirtualization 改善 | [C++ Team Blog](https://devblogs.microsoft.com/cppblog/msvc-build-tools-preview-updates-june-2026/) |
| 9 | Apple Developer Tools | WWDC 2026（6/9） | オンデバイスのカスタムモデル実行向け新フレームワーク「Core AI」、Foundation Models の Private Cloud Compute 無償提供・画像入力対応を発表 | [MacRumors](https://www.macrumors.com/2026/06/09/apple-outlines-major-ai-and-developer-tool-updates/) |
| 10 | Next.js | セキュリティ / バックポート修正（6月） | 複数の高・中・低 severity アドバイザリ対応、prerender 復旧・route params・route handlers・cache keys・client param parsing のコア修正 | [Next.js Updates](https://releasebot.io/updates/vercel/next-js) |

## Deep Dive

- [VS Code 1.124 — エージェントワークフローの強化](./tu-vscode-1-124.md)
- [GitHub Copilot SDK — agentic engine の GA と外部組込み](./tu-github-copilot-sdk-ga.md)
