# NVIDIA Rubinプラットフォーム — 次世代AIインフラの全貌

- **日付**: 2026-03-06
- **カテゴリ**: Tech
- **ソース**: [NVIDIA Newsroom](https://nvidianews.nvidia.com/news/rubin-platform-ai-supercomputer)

## 概要

NVIDIAが次世代AIプラットフォーム「Rubin」を発表した。6つの新チップとラック規模のAIスーパーコンピュータで構成され、推論トークンコストを最大10倍削減し、MoEモデル学習時のGPU数を4倍削減する。2026年後半からAWS・Google Cloud・Microsoft・OCIなどの主要クラウドプロバイダーが展開を開始予定。

## 詳細

### 6つのチップ構成

Rubinプラットフォームは以下の6つの新チップで構成される：

1. **NVIDIA Vera CPU** — 88個のカスタムOlympusコアを搭載。大規模AI工場向けに最適化された最高電力効率のCPU
2. **NVIDIA Rubin GPU** — 第3世代Transformer Engine搭載。推論用に50ペタフロップスの処理能力を提供
3. **NVLink 6 Switch** — GPU間通信用。各GPUで3.6TB/sの帯域幅を実現
4. **ConnectX-9 SuperNIC** — 高性能ネットワークインターフェース
5. **BlueField-4 DPU** — ストレージプロセッサとしてAI推論コンテキストの共有を実現
6. **Spectrum-6 Ethernet Switch** — 高帯域ネットワーク接続

### 主要製品構成

- **Vera Rubin NVL72**: 72個のRubin GPU + 36個のVera CPUを統合したラック規模システム。260TB/sの帯域幅を提供
- **HGX Rubin NVL8**: 8個のRubin GPUを搭載したサーバーボード。既存のデータセンターインフラに統合可能

### 性能向上

- 推論トークンコスト: 最大10倍削減
- MoEモデル学習: 必要GPU数を4倍削減
- 前世代（Blackwell）からの大幅な性能・効率向上

### 展開パートナーとスケジュール

2026年後半から以下のクラウドプロバイダーがRubinベースのインスタンスを展開予定：
- Amazon Web Services (AWS)
- Google Cloud
- Microsoft Azure
- Oracle Cloud Infrastructure (OCI)
- CoreWeave

### 市場環境

NVIDIAのデータセンター収益は直近四半期で前年比75%増の623億ドルに達している。半導体市場全体では2030年までに3〜4兆ドル規模への成長が見込まれている。一方で、Google・Amazonが独自のデータセンターチップを設計しており、NVIDIAの独占的地位への挑戦が続いている。

## 今後の注目点

- 2026年後半の実際の展開状況とパフォーマンスベンチマーク
- Google TPU、Amazon Trainiumなどカスタムチップとの競合関係の推移
- イラン紛争によるUAE・バーレーンのデータセンター被害がAIインフラ投資計画に与える影響
- Rubinプラットフォームの消費電力と冷却要件（エネルギー危機との関連）
- MetaやOpenAIなど大手AI企業の採用動向
