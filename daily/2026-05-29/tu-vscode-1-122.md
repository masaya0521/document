# VS Code — v1.122

- **日付**: 2026-05-28
- **カテゴリ**: Dev Tool
- **ソース**: [Release Notes v1.122](https://code.visualstudio.com/updates/v1_122), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/05/20/vs-code-1-121-adds-remote-agents-built-in-html-and-mermaid-previews.aspx)

## 概要

VS Code 1.122（2026年5月リリース）は、エージェント中心のワークフローと BYOK（Bring Your Own Key）の柔軟性をさらに高めるリリース。直近の 1.120（Agents Window を Stable 化）、1.121（リモートエージェントセッション、HTML/Mermaid プレビュー内蔵）に続き、5月だけで 3 バージョンが立て続けにリリースされた。今回の目玉は、GitHub サインインなしで自前の言語モデルを使える「Air-gapped BYOK」と、統合ブラウザでのデバイスエミュレーションによる Web アプリのレスポンシブテスト機能。

## 主な変更点

### 言語モデル（BYOK）
- **Air-gapped BYOK**: GitHub サインイン不要で自前の言語モデルを利用可能に。エアギャップ環境やオフライン環境のワークフローに対応。
- カスタムエンドポイントプロバイダーが Stable 版に昇格。
- API キーの更新・モデル追加など、粒度の細かいプロバイダー管理アクションを提供。
- `Manage Language Models` コマンドを Agents Window から実行可能に。

### 統合ブラウザ
- **デバイスエミュレーション**: 画面サイズ、モバイル/タッチエミュレーション、カスタム User-Agent に対応し、統合ブラウザ内で Web サイトのレスポンシブ挙動をテスト可能。
- **スクリーンショット添付**: ブラウザビューポートのスクリーンショットをチャットコンテキストに添付できる。

### エージェント関連
- Agents Window にセッションのホバー詳細表示を追加。Local VS Code harness（Insiders のみ）をサポート。
- ローカルエージェントセッションが OpenTelemetry 信号（`github.copilot.*` 属性）を発行し、可観測性を強化。

### その他
- **リッチな Issue 報告**: スクリーンショットやビデオ録画を含められる新しい Issue 報告ウィザード。

## 今後の注目点

- 5月の 3 連続リリース（1.120〜1.122）が示すように、VS Code は「エージェントファースト」な IDE へと急速にシフトしている。Agents Window が中心的な UI になりつつある。
- Air-gapped BYOK はエンタープライズ／規制環境での AI 活用を後押しする。社内 LLM との接続を前提とした運用が広がる可能性。
- 統合ブラウザのデバイスエミュレーション・スクリーンショット連携により、エージェントによる UI テスト・修正のループが IDE 内で完結する方向に進んでいる。
