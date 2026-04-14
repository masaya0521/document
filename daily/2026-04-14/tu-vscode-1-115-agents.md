# VS Code 1.115 — エージェントネイティブ開発の幕開け

- **日付**: 2026-04-08
- **カテゴリ**: Dev Tool
- **ソース**: [Release Notes](https://code.visualstudio.com/updates/v1_115), [InfoWorld](https://www.infoworld.com/article/4156169/visual-studio-code-1-115-introduces-vs-code-agents-app-2.html)

## 概要

VS Code 1.115 は、エージェントネイティブな開発体験を本格的に推進するリリース。新たに **VS Code Agents** コンパニオンアプリ（プレビュー）を導入し、複数リポジトリにまたがるエージェントセッションの並列実行を可能にした。統合ブラウザとターミナルのエージェント連携も強化され、AI エージェントがより自律的に開発タスクをこなせる環境が整いつつある。

## 主な変更点

### VS Code Agents アプリ（プレビュー）

VS Code Insiders と並行して動作する新しいコンパニオンアプリ。主な特徴:

- 複数リポジトリで**エージェントセッションを並列実行**（各セッションは独立した worktree で分離）
- セッション進捗の追跡、インライン diff の確認
- エージェントへのフィードバック送信
- アプリ内から直接 **Pull Request を作成**
- 既存のカスタム指示やプロンプトファイルの設定を引き継ぎ

### 統合ブラウザの改善

- ツールコールのラベルがより説明的に（実際のアクションとターゲットタブへのリンクを表示）
- 長時間実行スクリプトの安定性向上
- エージェントによる重複タブ開設の削減
- macOS でのピンチズーム対応

### ターミナルツールの拡張

- `send_to_terminal` ツールで**バックグラウンドターミナルへの入力送信**が可能に
- バックグラウンドターミナルのコマンド完了時に自動通知（終了コードと出力を含む）
- ユーザー入力が必要な場合の検出・通知機能（実験的）

### Copilot BYOK（Bring Your Own Key）

- Copilot Business / Enterprise ユーザー向けに、**独自の API キーで外部 LLM を利用可能**に
- 対応プロバイダ: OpenRouter, Ollama, Google, OpenAI など

### その他の改善

- テストカバレッジのミニマップ表示
- ターミナルへのファイルペースト（Ctrl+V / ドラッグ＆ドロップ）
- エディタの一般的な安定性・パフォーマンス改善

## 今後の注目点

- VS Code Agents アプリの安定版リリース時期
- エージェントセッションの worktree 分離がチーム開発ワークフローに与える影響
- BYOK 機能の個人ユーザー（Free / Pro）への展開
- JetBrains の ACP（Agent Client Protocol）対応と合わせた、IDE のエージェントプラットフォーム化の流れ
- GitHub Copilot cloud agent の検証ツール高速化（同週発表）との連携
