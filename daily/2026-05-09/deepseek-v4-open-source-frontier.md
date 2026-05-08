# DeepSeek V4 Preview とオープンソース・フロンティア競争

- **日付**: 2026-05-09（V4 Preview 公開は 2026-04-24、5月に入ってからは Hugging Face 経由のエコシステム展開が加速）
- **カテゴリ**: Tech
- **主要ソース**: [DeepSeek API Docs](https://api-docs.deepseek.com/news/news260424) / [Hugging Face: DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) / [MIT Technology Review](https://www.technologyreview.com/2026/04/24/1136422/why-deepseeks-v4-matters/) / [Fortune](https://fortune.com/2026/04/24/deepseek-v4-ai-model-price-performance-china-open-source/) / [CNBC](https://www.cnbc.com/2026/04/24/deepseek-v4-llm-preview-open-source-ai-competition-china.html)

## 概要

DeepSeek が 2026-04-24 に V4 Preview を公開し、5月にかけて V4-Pro（1.6T MoE / 49B 活性）と V4-Flash（284B / 13B 活性）の双方が API・チャット・アプリで利用可能になった。両モデルは 1M トークンコンテキストと Thinking / Non-Thinking 二系統のモードを持ち、MIT ライセンスで重みが公開されている。Huawei 製 AI チップとの最適化が深く、推論コストはフロンティア閉塞モデルから「桁違いに安い」と各種ベンチで評価された。同日 Moonshot Labs も Kimi K2.6 を、NVIDIA も Nemotron / Cosmos / Alpamayo / Isaac GR00T / Clara を相次いで開放しており、2026 年は「フロンティア性能のオープン化」が一気に進む年になりつつある。

## 詳細

### V4 のモデル構成

- DeepSeek-V4-Pro: 1.6T パラメタ MoE、活性 49B、1M コンテキスト
- DeepSeek-V4-Flash: 284B パラメタ MoE、活性 13B、1M コンテキスト
- 両モデルとも Thinking / Non-Thinking 二系統を内蔵し、推論時にユーザがコスト・遅延を選択可能
- ライセンス: MIT（商用利用・派生・ファインチューニング自由）
- 配布: Hugging Face で重み公開、API/チャット/アプリで即利用可

### 性能と価格

- Fortune によれば API 推論価格は閉塞モデルの数分の1〜数十分の1のレンジ
- MIT Technology Review は「V4 はオープン重み陣営として、複数のリーダーボードで GPT-5/Claude 4.6 のスコアに肉薄するレベルに到達した」と評価
- ただし長コンテキスト時の確からしさ・幻覚率や、コードエージェント領域での実利用品質は閉塞モデルが依然優位という指摘もあり、用途別の使い分けが現実解

### Huawei スタックとの結合

- Fortune は「V4 は Huawei の Ascend 系 AI チップとの統合最適化が深い」と報じ、米国の輸出規制下でも中国国内で大規模学習・推論が完結する設計を重視。
- これは単なるオープンソース戦略ではなく、輸出管理 vs 国産スタックの構造的な競争でもあり、米中AI分断の長期的な触媒になり得る。

### 同時期に進む「オープン化のラッシュ」

- Moonshot Labs: Kimi K2.6 公開 + Kimi Vendor Verifier（推論ベンダの精度検証ツール）も OSS 化
- NVIDIA: Nemotron（agentic）、Cosmos（physical AI）、Alpamayo（自動運転）、Isaac GR00T（ロボティクス）、Clara（医療）の open model/data/tool を一括公開
- OpenAI: Symphony（Codex エージェントが Linear チケットからマージまで自走するためのオープン仕様）
- 「クローズドはアプリ層」「オープンはモデル＆プロトコル層」という分業が見え始めた

### 開発者・企業視点の意味

- ローカル推論・自社クラウド推論で「フロンティア性能 × 1M コンテキスト」が現実コストで使えるようになった
- 規制上の理由（データレジデンシー、医療、金融、政府）でクローズドAPIを使えなかったセグメントへの浸透が加速
- ファインチューニング・蒸留の素材として、企業内タスクへの最適化のベースモデルとしての利用余地が大きい

## 今後の注目点

- V4 Preview から GA への移行スケジュールと、Pro/Flash 以外の派生（V4-Mini、V4-Code 等）の登場
- ベンチマークだけでなく、実運用（長コンテキスト忠実度、エージェント連携、ツール呼び出し）での閉塞モデルとのギャップ縮小度
- Huawei Ascend 連携の深化が、中国外（特に APAC・中東）の AI インフラ選択にどう影響するか
- 米政府の AI モデル「FDA型」事前審査がオープン重みモデルにどう適用されるか（公開後の改変・蒸留版にどこまで規制を及ぼせるか）
- OpenClaw や Symphony と組み合わせた「オープン重みモデル + オープンエージェントスタック」の競争力が、Cursor / Claude Code 等のクローズドツールにどこまで迫るか
