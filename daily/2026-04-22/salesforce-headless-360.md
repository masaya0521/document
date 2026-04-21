# Salesforce Headless 360 とエージェントファースト戦略

- **日付**: 2026-04-22
- **カテゴリ**: Tech
- **ソース**: [Salesforce](https://www.salesforce.com/news/stories/salesforce-headless-360-announcement/) / [VentureBeat](https://venturebeat.com/technology/salesforce-launches-headless-360-to-turn-its-entire-platform-into-infrastructure-for-ai-agents) / [The Register](https://www.theregister.com/2026/04/15/salesforce_headless_360/) / [Salesforce Ben](https://www.salesforceben.com/salesforce-headless-360-and-agentforce-vibes-2-0-revealed-at-tdx-2026/)

## 概要

Salesforce は 2026 年 4 月 15 日、TrailblazerDX 2026（TDX 2026）で「Headless 360」を発表した。CRM・サービス・マーケティング・EC といった Salesforce プラットフォームの全機能を **API / MCP ツール / CLI コマンド** として公開し、AI エージェントがブラウザ UI を一切開かずに業務を完遂できる設計にシフトする。

この発表は「SaaS は画面で使うもの」という前提を根本から塗り替える姿勢の表明であり、同時期に発表された AgentExchange（エージェント配布マーケット）、Agentforce Vibes 2.0（マルチモデル対応 IDE）、Agent Script（エージェント定義 DSL）と併せ、Salesforce がエージェントファースト SaaS インフラへ舵を切ったことを示す。

## 詳細

### 3 本柱の構造

1. **Developer Access**: 60 以上の MCP ツールと 30 以上のコーディングスキルを同時投入。Claude Code / Cursor / Codex / Windsurf などのコーディング環境から、UI を触らずに Salesforce プラットフォーム全体にアクセスできる。
2. **Experience Layer（Agentforce Experience Layer）**: エージェントの動作と表示を分離する UI サービス。フライト状況カード・リブッキングフロー・判断タイル等のインタラクティブ要素を Slack / Teams / Mobile / ChatGPT / Claude / Gemini など MCP 対応クライアントでネイティブ描画可能。
3. **Agent Governance**: エージェントのライフサイクル管理ツール群（テスト・評価・実験・観測・オーケストレーション）と、決定論的な挙動定義 DSL「Agent Script」を GA かつオープンソース化。

### 戦略的意義

- **"Browser-less" SaaS**: 人間は Slack / Teams などの会話型 UI に留まり、バックエンド業務はエージェントが API / MCP 経由で処理する構図を想定。画面クリック数で課金されてきた SaaS ビジネスモデル（席数ベース）が、エージェント API 呼び出しベースへと移行する可能性を示唆。
- **MCP への賭け**: 100 超のツール群を MCP として公開することで、Anthropic が提唱した MCP がエンタープライズ SaaS 統合レイヤーのデファクトになるかが焦点。ベンダーロックイン回避と AI 各社の同時サポートを狙う。
- **Agent Script のオープン化**: エージェント挙動を IaC 的に宣言記述するデファクト獲得を狙う。TerraForm 的なポジションを目論む動き。

### 周辺の温度感

競合の ServiceNow / HubSpot / Oracle も同時期にエージェント対応を進めており、「UI 越しに使う SaaS」から「エージェント前提 SaaS」への再設計競争は 2026 年後半のエンタープライズ IT 最大のテーマになりつつある。一方で、Agentforce Vibes 2.0 が Salesforce スタック内でしか完結しないとビルダーとエコシステムの分断（Builder Gap）を広げるという指摘も出始めた。

## 今後の注目点

- MCP 経由でのエージェント運用の SLA・監査・権限設計（DLP、行レベル ACL 連携）
- AgentExchange 上でのサードパーティスキル流通の動向
- Agent Script が AWS / Azure / Google Agent 基盤にポータブルに乗るか
- 競合（ServiceNow / Microsoft Dynamics / HubSpot）のエージェントファースト再設計のタイミング
- 「座席課金」から「エージェント呼び出し課金」への Salesforce 課金体系の再定義
