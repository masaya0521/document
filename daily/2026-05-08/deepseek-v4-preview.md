# DeepSeek V4 プレビュー — フロンティアとの差を埋める "格安巨大モデル"

- **日付**: 2026-05-08
- **カテゴリ**: Tech
- **ソース**:
  - [DeepSeek V4 Preview Release — DeepSeek API Docs](https://api-docs.deepseek.com/news/news260424)
  - [DeepSeek previews new AI model that 'closes the gap' with frontier models — TechCrunch](https://techcrunch.com/2026/04/24/deepseek-previews-new-ai-model-that-closes-the-gap-with-frontier-models/)
  - [DeepSeek V4 Pro (Max) — Artificial Analysis](https://artificialanalysis.ai/models/deepseek-v4-pro)

## 概要

DeepSeek が公開したプレビュー版 **DeepSeek-V4** は、Pro が **総パラメータ 1.6T / 活性 49B**、Flash が 284B / 活性 13B の MoE 構成で、いずれも **コンテキスト長 1M トークン** に対応する。SWE-bench Verified で 80.6% (Claude Opus 4.6 と 0.2 ポイント差) を主張し、価格は出力トークンあたり Claude Opus 4.6 の **約 1/7**。「フロンティアに肉薄しつつ桁違いに安い OSS 系列」という路線が一段階進んだ格好で、エンタープライズの推論コストの想定を再び塗り替えうる発表となった。

## 詳細

### モデル構成

| モデル | 総パラメータ | 活性パラメータ | コンテキスト | 主な狙い |
|--------|--------------|------------------|----------------|------------|
| DeepSeek-V4-Pro | 1.6T | 49B | 1M トークン | 推論・コーディング上限性能 |
| DeepSeek-V4-Flash | 284B | 13B | 1M トークン | 低レイテンシ / 低価格レイヤー |

MoE 構成のためアクティブ重みは小さく、推論時のメモリ帯域・電力要求は総パラメータほど跳ね上がらない設計。

### ベンチマーク

- **SWE-bench Verified: 80.6%** — Claude Opus 4.6 (80.8%) と僅差。
- 一部の推論タスクでは GPT-5.2 / Gemini 3.0 Pro を上回ると主張。
- 1M コンテキストで long-context 評価 (例えば repo-level コード理解) のスコアも改善傾向。

### 価格

| モデル | Input (cache hit) | Input (cache miss) | Output |
|--------|---------------------|----------------------|----------|
| DeepSeek-V4-Pro | $0.145 / Mtok | $1.74 / Mtok | $3.48 / Mtok |
| DeepSeek-V4-Flash | $0.028 / Mtok | — | $0.28 / Mtok |
| Claude Opus 4.6 (参考) | $5 / Mtok | — | $25 / Mtok |
| GPT-5.4 (参考) | $2.50 / Mtok | — | $15 / Mtok |

コーディング系ベンチが Claude Opus 4.6 と並ぶ水準で、出力単価が **約 1/7** という構図。Flash はさらにもう 1 桁安い。

### 戦略的インパクト

- **OSS 系列の "実用品質" 再定義**: V3 で価格破壊を見せた DeepSeek が、V4 で「フロンティア性能 × OSS × 低価格」に踏み込んだ。Llama 系列や Kimi K2.6、Gemma 4 と合わせ、フロンティア独占の構図が緩む方向。
- **MoE 推論インフラの重要性**: 1.6T 級モデルを商業的に配信するには、Google TPU 8i の SRAM 増強や Cerebras の wafer-scale など、MoE 向き推論アクセラレータの優位性がそのまま価格競争力に直結する。
- **エンタープライズの自前ホスティング選択**: API 価格だけでなく、ライセンスとデータ統制の観点で「自社クラスタで V4 系列を動かす」選択肢が現実味を帯びる。
- **規制 / ガバナンス**: 中国発の高性能モデルである点は、欧米の輸出管理・データ主権の観点で引き続き論点になる。

## 今後の注目点

- **正式版 (GA) のスペック差**: プレビューと最終版でベンチや価格、コンテキスト長が変わるか。
- **推論パートナーの拡大**: Together / Fireworks / Groq などが V4 をホスティングするか、価格はどうなるか。
- **ライセンス条件**: V3 と同様の商用利用可ライセンスが維持されるか、用途制約が追加されるか。
- **Vendor Verifier 系 OSS との連携**: Moonshot の Kimi Vendor Verifier のような「ホスティング先の品質を検証する」ツールが、DeepSeek でも整備されるか。
- **コーディングエージェントとの統合**: SWE-bench 80% 級が安価に使えると、Cursor / Cline / Roo Code 等のエージェントの既定モデル分布が変わる可能性。
