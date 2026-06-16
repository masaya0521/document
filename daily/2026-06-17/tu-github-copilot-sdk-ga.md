# GitHub Copilot SDK — 一般提供開始（GA）

- **日付**: 2026-06-17
- **カテゴリ**: Dev Tool
- **ソース**: [GitHub Changelog - Copilot SDK GA](https://github.blog/changelog/2026-06-02-copilot-sdk-is-now-generally-available/)

## 概要

2026年6月2日、GitHub Copilot SDK が一般提供（GA）になった。これにより開発者は、Copilot の agentic engine（自律エージェントの実行基盤）を自前のアプリケーション・サービス・開発者ツールに、安定した API と本番対応サポート付きで組み込めるようになった。Copilot を「IDE 上のアシスタント」から「あらゆるプロダクトに埋め込める部品」へと拡張する動きで、エージェント機能の内製化を進めたいチームにとって重要なマイルストーンとなる。

## 主な変更点

### 対応言語（6言語）

- Node.js / TypeScript
- Python
- Go
- .NET
- **Rust**（GA で新規追加）
- **Java**（GA で新規追加）

### 主な機能

- **カスタムツールと MCP 対応**: エージェントが自律的に実行できるツールの登録、および Model Context Protocol サーバーへの接続に対応
- **システムプロンプトのカスタマイズ**: identity・tone・tool instructions・safety rules などをセクション単位で編集可能
- **OpenTelemetry トレーシング**: W3C trace context の伝播に対応し、エージェントの挙動を可観測化
- **柔軟な認証**: GitHub OAuth、GitHub Apps、環境トークン、複数プロバイダーの BYOK（Bring Your Own Key）に対応
- **クラウド・リモートセッション**: リポジトリメタデータ付きのセッション作成に対応

## ユースケース

プレビュー期間中は、CI/CD 支援ツール、社内開発ツール、顧客向け AI 機能などへの組込みに利用された。GA 時点では、既存の Copilot 購読者・Copilot Free 利用者・自社モデル利用ユーザーが対象。

## 今後の注目点

- MCP 対応により、既存の MCP エコシステム（各種データソース・ツール連携）をそのまま Copilot エージェントに接続できる点が普及の鍵
- BYOK 対応で、Copilot の実行基盤を使いつつモデルは自社契約のものを使う、というハイブリッド構成が可能に
- VS Code 1.124 の Agents ウィンドウや Copilot CLI の機能拡張と合わせ、GitHub のエージェント戦略が「IDE・CLI・SDK」の三層で揃いつつある
