# フロンティアAIモデル競争が一気に加速した4月

- **日付**: 2026-04-24
- **カテゴリ**: Tech
- **ソース**:
  - [devFlokers: AI News Last 24 Hours, April 2026](https://www.devflokers.com/blog/ai-news-last-24-hours-april-2026-model-releases-breakthroughs)
  - [NxCode: DeepSeek V4 Release Specs](https://www.nxcode.io/resources/news/deepseek-v4-release-specs-benchmarks-2026)
  - [Fazm: Open Source AI Projects April 2026](https://fazm.ai/blog/open-source-ai-projects-releases-updates-april-2026)

## 概要

2026 年 4 月はフロンティア AI モデルの発表が異常な密度で重なり、わずか 12 日間のうちに Meta・Alibaba・Google・Mistral・Ai2 から 7 つのメジャー OSS モデルが出揃った。加えて閉鎖系では Anthropic の Claude Mythos 5（10T パラメータ級）と OpenAI の GPT-5.4 系列、オープン系では DeepSeek V4（1T MoE）が揃い、「人間相当のデスクトップタスク処理」が現実の議題に乗り始めた月になった。

## 詳細

### Claude Mythos 5（Anthropic）

Anthropic は 2026 年 4 月に Claude Mythos 5 を投入した。主な特徴は次の通り。

- 10 兆パラメータクラスの公に認知された初のモデル。
- ハイステークス領域（サイバーセキュリティ、学術研究）向けに設計。
- 同月、Mythos 自体への不正アクセスの疑いがあるとして Anthropic が社内調査を実施中であることも明らかに。

ポイントは、ハッカーに利益をもたらし得るレベルの攻撃能力を内包しうるモデルを、リリース直後に自社のセキュリティ事故として扱わざるを得なかった点にある。「モデル自身のガバナンス」と「モデルを守るインフラのガバナンス」が同じ速度で求められる時代に入った。

### GPT-5.4 系列（OpenAI）

- GPT-5.4 "Thinking" 版が、OSWorld-Verified（ブラウザ・デスクトップ操作ベンチ）で 75.0% を記録し、人間水準を初めて越えた。
- OpenAI は同月、GPT-5.4-Cyber（防御系サイバーセキュリティ特化版）も投入。
- Codex 側では週次開発者数が 3M → 4M に 2 週間で拡大し、SDLC 全般への展開が進む。

モデル単体の能力競争は既に「マルチステップの作業代行」ができるかに軸足が移り、"agentic" を冠するベンチマークと実運用の両方で同時に進行している。

### DeepSeek V4（DeepSeek）

- 約 1 兆パラメータの MoE。トークン毎のアクティブは約 370 億で MoE の効率を維持。
- Engram 条件付きメモリに基づく 1M トークンコンテキスト。
- テキスト・画像・動画のネイティブマルチモーダル生成。
- 重みを Apache 2.0 で公開予定（コメント: 公開日・V4 モデル ID は 4 月 11 日時点で正式には未確定であり、公式リリースを要確認）。
- 内部ベンチマークは SWE-bench Verified で約 81%（第三者評価ではない）。
- 推論価格は $0.30/MTok 目線と低く、INT8/INT4 量子化でデュアル RTX 4090 程度での運用も視野。

DeepSeek V4 は「米フロンティアに追随する OSS が、MoE + 公開重み + 価格」の 3 点で仕掛けている構図がそのまま 4 月に表面化した事例である。学習費用も $5.2M 級と報じられ、資本集約度の差で競争優位が決まるわけではないことを改めて示した。

### 他の OSS 勢

- **GLM-5.1**（4/7 リリース、MIT ライセンス、754B MoE）: 長時間エージェントタスク向け。
- **Gemma 4**（4/2 リリース、Apache 2.0）: Gemmaverse として初の OSI 準拠 Apache 2.0 採用。
- vLLM と llama.cpp も 4 月前半で複数のアップデート。
- Linux Foundation の Goose 1.2 は自動 MCP サーバ発見とローカル優先実行を強化。

## 今後の注目点

- **agentic ベンチの有効性**: OSWorld-Verified のような操作系ベンチが「人間を超えた」と宣伝され始める一方、ドメイン固有タスクで本番に耐えるかは未知。運用データに基づく評価の標準化が鍵。
- **オープン重みと地政学**: DeepSeek V4 や GLM-5.1 のような「フル Apache 2.0」が増えるほど、輸出規制や国家安全保障上の議論は再加速する。
- **モデル基盤自体のセキュリティ**: Mythos への不正アクセス疑惑のように、モデル重み・推論プラットフォームに対する攻撃は今後「AI セキュリティ」の中核領域になる。
- **コスト**: 学習コスト $5M 級が事実なら、フロンティア競争の入場料はこの半年で一段下がる可能性がある。推論コスト（$/MTok）との組み合わせで勝敗が決まる局面。
- **エンタープライズの本番投入速度**: Google Cloud Next 2026 で 500 社超が agentic Gemini を本番投入していると発表されており、PoC から production への移行が観測できる水準に入ってきた。
