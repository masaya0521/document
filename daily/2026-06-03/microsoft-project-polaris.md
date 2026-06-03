# Microsoft「Project Polaris」— GitHub Copilot から OpenAI を切り離す自社製コーディングモデル

- **日付**: 2026-06-03
- **カテゴリ**: Tech
- **ソース**: [TechTimes](https://www.techtimes.com/articles/317596/20260602/github-copilot-replaces-gpt-4-project-polaris-ships-multi-agent-vs-code-build.htm) / [FourWeekMBA](https://fourweekmba.com/ai-microsoft-project-polaris-replaces-openai-copilot/) / [ChatForest](https://chatforest.com/builders-log/microsoft-build-2026-recap-windows-agent-platform-project-polaris-copilot-workspace/)

## 概要

Microsoft は Build 2026（6/2〜6/3、サンフランシスコ Fort Mason Center）で、自社製の AI コーディングモデル「Project Polaris」を発表した。Polaris は2026年8月から GitHub Copilot の既定エンジンとして GPT-4 Turbo を置き換える予定で、Microsoft にとって最も広く使われる開発者製品を OpenAI 依存から切り離し、エンドツーエンドの自社所有へ移行する大きな転換点となる。

同時に「a peer programmer, not a pair programmer（ペアではなくピアのプログラマ）」というポジショニングを掲げ、バグ・機能・保守タスクを割り当てて自律的に完遂させる方向性を打ち出した。

## 詳細

### アーキテクチャと性能

Polaris は Mixture-of-Experts（MoE）アーキテクチャを採用し、プログラミング言語・フレームワークごとに最適化されたサブモジュールを持つ。Microsoft によれば HumanEval と MBPP のベンチマークで GPT-4 Turbo を上回り、特に Rust や Haskell といった低リソース言語で顕著な改善が見られるという。

推論時には chain-of-thought プロンプティングと tree-of-thought 探索による高度な推論を組み込み、従来の AI アシスタントが苦手としてきた複数ファイルにまたがる大規模リファクタリングに対応する。

### インフラとコスト

モデルは Azure 内の自社 AI アクセラレータ「Maia」上で動作する。Microsoft はこれにより推論あたりのレイテンシ削減とコスト低減を実現したとしている。OpenAI のモデル利用に伴うライセンスコストを排除しつつ、自社チップ・自社モデル・自社クラウドの垂直統合を進める狙いが透ける。

Polaris はコード生成・複数ファイルリファクタリング・テスト記述・コードレビュー・ドキュメント生成・依存関係分析といった開発タスク専用に設計されている。

### マルチエージェント VS Code

Build では「マルチエージェント VS Code」も発表された。プランナーとスペシャリストの構造を導入し、オーケストレータが目的を分解してサブエージェントに委譲、統一インターフェース上で結果を提示する。開発者はリアルタイムの進捗を監視し、主タスクのコンテキストを失わずに実行途中で軌道修正できる。

### 移行スケジュール

GPT-4 Turbo からの置き換えは2026年8月開始。全 Copilot サブスクライバーが自動移行され、3ヶ月のフォールバック期間がオプションで提供される。

### その他の Build 2026 発表

- Windows Agent Framework 1.0
- Azure Agent Mesh
- Copilot Workspace の一般提供
- Office 365 Copilot の Agent Mode 既定化
- Foundry Local の一般提供
- Azure AI Foundry が Claude / DeepSeek / Llama / Mistral をサポート

## 今後の注目点

- 8月の本番移行時に GPT-4 Turbo 比でユーザー体験・コード品質が実際に向上するか
- OpenAI との関係性への影響（Microsoft は依然 OpenAI の大株主）
- Claude Code や Cursor 等、自律型コーディングエージェント市場での競争激化
- Maia アクセラレータの量産・供給が推論需要に追従できるか
- 「自律的にタスクを完遂するエージェント」という主張が、実運用でどこまで信頼できるか
