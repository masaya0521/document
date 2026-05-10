# DeepSeek V4: Huawei チップで動く 1.6 兆パラメータ・モデルが示す新しい AI 経済学

- **日付**: 2026-05-10
- **カテゴリ**: Tech
- **ソース**:
  - [DeepSeek V4 Preview Release | DeepSeek API Docs](https://api-docs.deepseek.com/news/news260424)
  - [Tom's Hardware: DeepSeek launches 1.6 trillion parameter V4 on Huawei chips](https://www.tomshardware.com/tech-industry/artificial-intelligence/deepseek-launches-1-6-trillion-parameter-v4-on-huawei-chips-as-us-escalates-ai-theft-accusations)
  - [TechCrunch: DeepSeek previews new AI model that 'closes the gap' with frontier models](https://techcrunch.com/2026/04/24/deepseek-previews-new-ai-model-that-closes-the-gap-with-frontier-models/)

## 概要

中国の AI 企業 DeepSeek は 2026 年 4 月 24 日、3 度の延期を経て新フラッグシップモデル **DeepSeek-V4-Pro / V4-Flash** のプレビューをリリースした。1.6 兆パラメータ規模ながら 1M トークンのコンテキスト、Huawei Ascend AI プロセッサ向け最適化、$3.48/1M 出力トークンという破格の価格——これらが組み合わさることで、AI モデル経済の前提条件を揺さぶる存在になっている。

特筆すべきは、**フロンティア級のモデルが Nvidia ではなく Huawei のハードウェアでトレーニング・推論される**点で、米中の AI 半導体規制の構図を反映した象徴的なリリースとも言える。

## 詳細

### モデル仕様

| モデル | 総パラメータ | アクティブパラメータ | コンテキスト |
|---|---|---|---|
| V4-Pro | 1.6T | 49B | 1M tokens |
| V4-Flash | 284B | 13B | 1M tokens |

両モデル共に 32 兆トークン以上の精選済みデータで事前学習されている。

### アーキテクチャの革新: CSA + HCA

V4 では従来の full attention を廃し、**Compressed Sparse Attention (CSA)** と **Heavily Compressed Attention (HCA)** のハイブリッドを採用した。これにより:

- 単一トークン推論の FLOPs: V3.2 比で **27%** に削減
- KV キャッシュサイズ: V3.2 比で **10%** に削減

長コンテキスト (1M トークン) を扱う際の推論コストを劇的に下げる設計で、エージェント用途や大量ドキュメント処理に適している。

### 価格破壊

| モデル | $/1M output |
|---|---|
| DeepSeek V4-Pro | $3.48 |
| DeepSeek V4-Flash | $0.28 |
| OpenAI GPT-5.4 | $30 |
| Anthropic Claude Opus 4.6 | $25 |

V4-Pro は GPT-5.4 比で約 **1/9**、Flash は **1/100** 以下の価格水準。性能ベンチマークがフロンティアに「肉薄」とされる中、コスト効率は他社を圧倒する。

### Huawei Ascend 対応の地政学的意味

米国が中国向け Nvidia 高性能 GPU の輸出規制を強化している中、DeepSeek は **国産 Huawei Ascend に最適化したフロンティアモデル** をリリースした。これは:

1. 中国国内での AI モデル開発・運用が Nvidia 依存から脱却可能であることを示す技術的実証
2. 米政府が DeepSeek 含む中国 AI 企業に「IP 窃取」の疑いをかけ調査を強化する局面でのリリース
3. 開発エコシステム（CUDA 中心）が他チップに広がる契機になりうる

## 今後の注目点

- **オープンウェイト公開のタイムライン**: プレビュー段階だが、過去の DeepSeek 同様のオープンウェイト公開があるか
- **ベンチマーク詳細の精査**: 「フロンティアに肉薄」が公開時の独立評価で再現されるか
- **Huawei Ascend エコシステムの成熟度**: PyTorch 等のフレームワーク互換性、開発ツール、サポート体制
- **米政府の対抗措置**: IP 窃取調査の進展、追加制裁、Huawei 関連企業のエンティティリスト追加など
- **エージェント用途での実利用**: 1M コンテキスト × 低コストの組み合わせがエージェントの長期記憶ワークロードを変えるか
- **国内 (日本含む) 利用の制約**: 中国製モデル利用に関する企業ポリシー・規制動向
