# Visual Studio Code 1.116 — Copilot 同梱と Agent 開発環境の刷新

- **日付**: 2026-04-20（リリース日: 2026-04-15）
- **カテゴリ**: Dev Tool / Editor
- **ソース**: [VS Code 1.116 Release Notes](https://code.visualstudio.com/updates/v1_116), [Release Notes Archive](https://code.visualstudio.com/updates/archive), [Releasebot: VS Code](https://releasebot.io/updates/microsoft/visual-studio-code)

## 概要

VS Code は 2026 年から週次リリース体制に移行しており、1.116 はその継続リリース。本バージョンでは **GitHub Copilot Chat 拡張が組み込み (built-in)** となり、新規ユーザーは拡張インストールなしに Chat / inline suggestions / agent を利用できるようになった。開発者向けとしては Agent 実行の観測性・制御性を高める一連の機能が追加されている点が大きい。

フロントエンド/バックエンド問わず、日常のエディタワークフロー全体に影響するため、CI のセットアップスクリプトや社内ガイドラインで「Copilot Chat 拡張のインストール手順」を案内しているチームは、記述の更新が必要になる。

## 主な変更点

### GitHub Copilot Chat の組み込み化

- 新規インストールでは Copilot Chat が最初から利用可能
- 既存環境では従来の拡張は `@builtin` 扱いとなり、拡張管理の UI から見える位置が変わる
- Enterprise の拡張機能制御（`extensions.allowed` 等）を使っている場合、ポリシーの再確認が推奨

### Agent Debug Logs

過去の agent セッションのログを閲覧できるビューが追加。以下が可能:

- ツール呼び出しの引数・結果の確認
- プロンプトと応答のペアの再生
- エラーで停止した箇所の再現調査

従来は Agent が「なぜそのツールを選んだのか」「なぜ失敗したのか」が不透明だったため、調査効率は顕著に上がる。

### Terminal Agent Tools

Agent セッションから任意のターミナルセッションを操作できるツールが追加。バックグラウンドで動作しているプロセスを対話的に扱えるため、長時間の dev server やログ監視を Agent 側から制御しやすい。

### Copilot CLI の Thinking Effort 設定

Copilot CLI でモデルの thinking effort を調整できるようになり、応答品質とレイテンシのトレードオフを明示的にコントロールできる。CI での利用時は低 effort、対話時は高 effort といった使い分けが実運用的に意味を持つ。

## 破壊的変更・移行ガイド

破壊的変更は少ないが、以下は確認したい。

- **カスタムキーバインド / 拡張 API**: Copilot Chat が built-in になったことで、一部のコマンド ID の前提が変わる可能性がある。自作拡張でコマンドに依存している場合は 1.116 でリグレッションテスト。
- **拡張機能ポリシー**: `github.copilot-chat` を明示的に無効化していた環境では、built-in 化により挙動が変わる。Enterprise の `chat.commandCenter.enabled` 等で制御する。
- **Agent 権限管理**: 1.111 以降で導入された agent permissions の概念は 1.116 で継続強化されている。プロジェクトごとに `.vscode/copilot.json`（想定）などの設定を共有する運用が現実的。

## 今後の注目点

- 週次リリースサイクルにより、月次メジャーアップデートから細粒度の改善フローへ移行。プロジェクト側は「VS Code バージョンを固定する運用」よりも「最新を追う運用」が現実解になりつつある
- Agent 関連機能は継続的に拡張されており、MCP との統合がさらに深まる見込み
- Copilot built-in 化に伴い、他の AI アシスタント拡張（Cursor 同梱系、Continue 等）との棲み分けが議論になる
