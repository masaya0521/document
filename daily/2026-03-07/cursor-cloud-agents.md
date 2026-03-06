# Cursor Cloud Agents — 自律型AIコーディングの新時代

- **日付**: 2026-03-07
- **カテゴリ**: Tech
- **ソース**: [TechCrunch](https://techcrunch.com/2026/03/05/cursor-is-rolling-out-a-new-system-for-agentic-coding/), [DevOps.com](https://devops.com/cursor-cloud-agents-get-their-own-computers-and-35-of-internal-prs-to-prove-it/)

## 概要

AIコーディングツールのCursorが、Cloud Agents（2月24日）とAutomations（3月5日）を相次いで発表し、自律型AIコーディングの新たな段階に突入した。隔離されたVM上でソフトウェアの構築・テスト・PR作成までを自律的に行うCloud Agentsは、社内PRの35%をエージェントが作成するまでに成長。ARRは20億ドルに到達し、AIコーディング市場の急拡大を象徴している。

## 詳細

### Cloud Agents の仕組み

2月24日に発表されたCloud Agentsは、完全に隔離された仮想マシン上で動作する自律型コーディングエージェント。主な特徴:

- **隔離VM実行**: 各エージェントが独自のVM環境を持ち、本番環境への影響なくソフトウェアを構築・テスト
- **ブラウザUIテスト**: エージェントがブラウザを操作してUIをナビゲートし、動作確認を自動実行
- **動画証跡**: 作業過程を動画で記録し、人間がレビュー可能な証跡を提供
- **PR自動作成**: マージ可能なPull Requestをアーティファクト付きでGitHubに直接作成

### Automations — イベント駆動型の常時稼働エージェント

3月5日に発表されたAutomationsは、外部トリガーに応じてエージェントを自動起動するシステム:

- **対応トリガー**: Slackメッセージ、Linear issue作成、GitHub PR マージ、PagerDutyインシデント、スケジュール実行
- **稼働規模**: 毎時数百のオートメーションが実行されている
- **ユースケース**: コードレビューの自動化、インシデント対応、新規issueのトリアージなど、単純なコード生成を超えた運用自動化

### 実績と数字

- **社内PR**: Cursor社内のマージ済みPRの35%がCloud Agentsによって作成
- **ARR**: 20億ドル（年間経常収益）に到達
- **市場ポジション**: GitHub Copilotに対する最有力な対抗馬として、エージェンティックなワークフローで差別化

### 競合状況

AIコーディングツール市場は急速に競争が激化:

- **GitHub Copilot**: MicrosoftのバックアップでIDE統合を強化
- **Claude Code**: Anthropicの対話型コーディングエージェント
- **Devin / Cognition**: 完全自律型のソフトウェアエンジニアを目指すアプローチ
- **Cursor**: Cloud AgentsとAutomationsで「開発ワークフロー全体の自動化」に舵を切る

### 開発者の採用状況

Stack Overflow 2025 Developer Surveyによると、開発者の84%がAIツールを使用中または使用予定、51%が毎日AIツールを使用していると回答。AIコーディングツールは既に「使うかどうか」ではなく「どれを使うか」のフェーズに入っている。

## 今後の注目点

- Automationsの対応トリガー拡大（CI/CDパイプライン統合、モニタリングツール連携など）
- Cloud Agentsの精度向上と、大規模コードベースでの実用性検証
- 「エージェントが作成したPR」の品質管理とレビュープロセスの標準化
- セキュリティ面の課題 — エージェントに付与する権限の管理とアクセス制御
- 競合各社（GitHub、Anthropic等）の対抗アクション
- 開発者のロールシフト — コードを書く役割からエージェントを監督・指示する役割への変化
