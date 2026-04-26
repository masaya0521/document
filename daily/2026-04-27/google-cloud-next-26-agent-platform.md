# Google Cloud Next '26: Gemini Enterprise Agent Platform と第8世代 TPU

- **日付**: 2026-04-27
- **カテゴリ**: Tech
- **ソース**: [Google Cloud Blog](https://cloud.google.com/blog/topics/google-cloud-next/welcome-to-google-cloud-next26), [Google Blog Recap](https://blog.google/innovation-and-ai/infrastructure-and-cloud/google-cloud/google-cloud-next-26-recap/), [Eighth-gen TPU 発表](https://blog.google/innovation-and-ai/infrastructure-and-cloud/google-cloud/eighth-generation-tpu-agentic-era/), [Virtualization Review](https://virtualizationreview.com/articles/2026/04/24/google-cloud-next-26-gemini-enterprise-agent-platform-leads-ai-centric-news.aspx), [SiliconANGLE](https://siliconangle.com/2026/04/20/google-cloud-next-2026-preview-real-story-isnt-ai-control-plane/)

## 概要

Google Cloud Next '26 で発表された目玉は、Vertex AI を統合・進化させた **Gemini Enterprise Agent Platform** と、エージェント時代向けに設計された **第8世代 TPU(8t/8i)** の二本柱。Google は AI 基盤の競争軸を「単一モデルの精度」から「エージェントを構築・運用・統治する制御プレーン」へと明確にシフトさせた。同時に Mira Murati 率いる Thinking Machines Lab とも数十億ドル規模の追加契約が報じられ、Nvidia GB300 + 自社 TPU という二系統の AI 基盤を持つ強みを前面に押し出している。

## 詳細

### Gemini Enterprise Agent Platform

プラットフォームは「build / scale / govern / optimize」の4軸で再構成された。主な構成要素:

- **Agent Studio / Agent Designer**: スケジュール・トリガー駆動でのエージェント設計
- **Agent Development Kit (ADK)**: エージェント実装のフレームワーク
- **Agent Runtime**: 長時間稼働エージェント向けの実行基盤
- **Agent-to-Agent Orchestration**: A2A プロトコルベースの協調実行
- **Agent Gateway / Agent Identity / Agent Registry**: 既存企業 IdP・API 管理層との接続点
- **Agent Observability / Simulation / Evaluation**: 本番運用に必要な可観測性とテスト

Gemini Enterprise app には Inbox(エージェント活動管理)、Skills(反復タスクの定型化)、Canvas(ファイル編集を画面切替なしに完結)などのエンドユーザー機能も搭載。Vertex AI のサービス群は順次 Agent Platform 経由での提供に移行する。

### 第8世代 TPU: 8t と 8i の役割分担

エージェント時代に向け、TPU は学習用と推論用で2チップ体制になった。

- **TPU 8t (training)**: 前世代比でほぼ3倍の演算性能。大規模モデルの学習時間を大幅短縮
- **TPU 8i (inference)**: エージェント・MoE ワークロード向けに極低レイテンシを実現。価格性能で前世代比+80%

ネットワーク・ストレージ側も同時にアップデート:

- **Virgo Networking**: TPU 8t を最大134,000チップ単一ファブリックで接続、47 Pbps の二分帯域
- **Managed Lustre**: 10 TB/秒のスループットで学習データの I/O ボトルネックを解消

### OSS / フレームワーク互換性の強化

- **PyTorch on TPU** がネイティブ対応化
- **vLLM** を GPU/TPU 双方で最適化サポート
- これにより Hugging Face エコシステムから TPU への移行コストが大幅低減

### パートナー戦略: 7.5億ドルのインセンティブ

Google は AI エージェント販売の促進に向け、コンサル・スタートアップ含む全パートナー向けの新規 $750M バジェットを発表。Gemini PoC、Forward Deployed Engineer 派遣、クラウドクレジット、デプロイメントリベートなどに充当できる。

### 競合構図

- **AWS Bedrock AgentCore / Microsoft Foundry Agent Service** に対し、Google は「Vertex AI から地続きの統合体験」を強みに据える
- Mira Murati の Thinking Machines Lab との大型契約は、外部 LLM ベンダーも自社 GPU・TPU で受け入れる「ハイパースケーラー回帰」を象徴
- Anthropic も AWS と Google で重複ホスティングしており、ハイパースケーラー間の AI 基盤覇権争いが鮮明化

## 今後の注目点

- **Vertex AI からの移行体験**: 既存ワークロードの非破壊な移行が実現するか。SDK 互換性と料金体系の整合が試金石
- **A2A プロトコルの標準化**: Anthropic の MCP との関係性、企業内エージェント連携での事実上の標準争い
- **TPU 8i の供給能力**: Nvidia GB300 が逼迫する中、自社 TPU で推論需要を吸収できるか。Gemini API の単価圧縮にも直結
- **ガバナンス層の競争力**: Agent Identity・Audit・Policy が金融・医療・公共領域での採用を左右。EU AI Act・米州法対応の早さが鍵
- **パートナーエコシステム**: $750M バジェットがコンサル系大手(Accenture・Deloitte)とブティック AI スタートアップのどちらに偏るかで、現場実装スタイルが分岐する可能性
- **エージェント評価基準**: Agent Evaluation/Simulation がデファクトのベンチマークになるか。SWE-bench/HumanEval に続く「エージェント版ベンチ」の議論が活発化する見込み
