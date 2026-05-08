# Google Cloud Next '26 — Gemini Enterprise Agent Platform と TPU 8

- **日付**: 2026-05-08
- **カテゴリ**: Tech
- **ソース**:
  - [Introducing Gemini Enterprise Agent Platform — Google Cloud Blog](https://cloud.google.com/blog/products/ai-machine-learning/introducing-gemini-enterprise-agent-platform)
  - [Google launches Gemini Agent Platform, eighth-generation TPUs — Computer Weekly](https://www.computerweekly.com/news/366641999/Google-launches-Gemini-Agent-Platform-eighth-generation-TPUs)
  - [7 highlights and announcements from Google Cloud Next '26 — Google Blog](https://blog.google/innovation-and-ai/infrastructure-and-cloud/google-cloud/google-cloud-next-26-recap/)

## 概要

Google Cloud Next '26 は 32,000 人以上が参加し、260 を超える発表があった "agentic era" 全面打ち出しのイベントとなった。中核は 2 つ。1 つは Vertex AI を進化させた **Gemini Enterprise Agent Platform**、もう 1 つは学習・推論で物理的に分かれた **第 8 世代 TPU (TPU 8t / TPU 8i)** である。エージェントを「作る」レイヤーと、それを「数百万単位で動かす」インフラを同時に刷新し、Google Cloud が年率換算 800 億ドル規模 (Q1 2026 売上 200 億ドル、前年比 +63%) の収益基盤を支えるための布石が揃った形になる。

## 詳細

### Gemini Enterprise Agent Platform

Vertex AI の後継として位置づけられ、モデル選択・モデル構築・エージェント構築を 1 つのワークスペースに集約する。エンタープライズ向けに以下のコンポーネントを提供する:

- **Agent Designer**: スケジュール / トリガー駆動のエージェントを GUI で組み立てる。
- **Long-running Agents**: 数時間〜数日に及ぶ業務プロセスを跨いで状態を保持。
- **Inbox**: ユーザがエージェントの活動を一覧・承認するハブ。
- **Skills**: 反復タスクをショートカット化、ライブラリとして再利用可能。
- **Canvas**: アプリ切り替えなしでファイル作成・編集を行うコラボ面。
- **Governance / Security**: 監査・データガバナンス・権限制御を統合。

OpenAI の Agent Builder や Microsoft の Agent Framework が先行する中、Google は「企業の既存 Vertex / Workspace ユーザがそのまま乗り換えられる」点を打ち出している。

### TPU 8t (Training)

- 1 スーパーポッド = 9,600 チップ + 2 PB の共有 HBM。
- ピーク 121 ExaFlops、前世代 (Ironwood) 比で約 3 倍のポッド演算性能。
- ストレージアクセスは前世代比 10 倍、Virgo Network + JAX + Pathways の組合せで **最大 100 万チップへ近線形スケール**。
- 性能/W は約 2 倍。

### TPU 8i (Inference)

- HBM 288 GB + on-chip SRAM 384 MB (前世代の 3 倍)。
- インターコネクト帯域 19.2 Tb/s、Mixture-of-Experts 推論を意識した設計。
- 新しい on-chip Collectives Acceleration Engine で内部レイテンシを最大 1/5 に削減。
- 性能/$ は前世代比 +80%。1,152 TPU を 1 ポッドにまとめ、低レイテンシで「数百万エージェントを同時稼働」できる経済性を狙う。

### 戦略的位置づけ

- 同時期発表の Intel との複数年提携、Gemma 4 の Apache 2.0 公開、Q1 2026 のクラウド市場 1,290 億ドル (+35%) という追い風と組み合わさり、Google は「モデル × インフラ × エージェント」を縦に統合する戦略を再強化。
- Nvidia GPU 寡占に対するハイパースケーラ自社シリコンの位置づけは、AWS Trainium/Inferentia や Microsoft の Maia と並び、より明確に「学習 vs 推論」に分業する潮流が固まりつつある。

## 今後の注目点

- **Vertex AI 既存ユーザの移行体験**: マイグレーションパスと価格モデルが現場で評価される 6〜12 ヶ月。
- **Agent Designer のロックイン度合い**: 他クラウド (Anthropic, OpenAI, AWS Bedrock Agents) との相互運用性は限定的になる可能性。
- **TPU 8 の歩留まりと供給**: 1 スーパーポッド級を本当に大規模配布できるかは Q3-Q4 のキャパ次第。
- **MoE 推論経済性**: TPU 8i の SRAM/インターコネクト強化が、DeepSeek V4 などの 1T 級 MoE をクラウドで安価に提供できる土台になるか。
- **Cerebras IPO や Nvidia GB300 系列との価格競争**: TPU 8 の "性能/$ 80% 改善" がそのまま競合の値下げ圧力になる可能性。
