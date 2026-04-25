# DeepSeek V4 — フロンティアモデルの 1/10 価格を実現した MoE と Hybrid Attention

- **日付**: 2026-04-26
- **カテゴリ**: Tech
- **ソース**:
  - [TechCrunch — DeepSeek previews new AI model that 'closes the gap' with frontier models](https://techcrunch.com/2026/04/24/deepseek-previews-new-ai-model-that-closes-the-gap-with-frontier-models/)
  - [Simon Willison — DeepSeek V4—almost on the frontier, a fraction of the price](https://simonwillison.net/2026/Apr/24/deepseek-v4/)
  - [DeepSeek API Docs — V4 Preview Release](https://api-docs.deepseek.com/news/news260424)
  - [CNBC — DeepSeek releases preview of long-awaited V4](https://www.cnbc.com/2026/04/24/deepseek-v4-llm-preview-open-source-ai-competition-china.html)

## 概要

中国の DeepSeek は 2026-04-24、長らく待たれていた DeepSeek V4 の Pro / Flash 2 種のプレビューを公開した。1.6T パラメータ（49B アクティブ）の Pro はオープンウェイトとして公開された最大級のモデルで、Kimi K2.6（1.1T）や GLM-5.1（754B）を上回る規模を持つ。MIT ライセンスで Hugging Face にウェイトが配布され、ローカル実行・微調整が可能。コンテキスト長は両モデルとも 1M トークン。

GPT-5.5（OpenAI）の発表からわずか 1 日後というタイミング、そして「フロンティアモデルとの差を 3〜6 か月程度まで縮めた」という DeepSeek 自身の評価が、米中 AI 競争の新たな緊張点を示している。

## 詳細

### モデル構成と効率改善

V4 は MoE（Mixture of Experts）構成で、さらに DeepSeek が「Hybrid Attention Architecture」と呼ぶ新たな設計を採用した。長い対話における過去クエリの記憶能力（=長文コンテキストの実用精度）を改善することを目的とする。

技術論文の自己申告では、V4-Pro は V3.2 比で

- **シングルトークン FLOPs を 27% に圧縮**
- **KV キャッシュサイズを 10% に圧縮**

しており、Flash はそれぞれ 10% / 7% とさらに極端な効率化を達成している。これが後述する破格の API 価格を可能にしている。

### ベンチマークでの位置づけ

DeepSeek は推論ベンチマークでオープン・クローズドの双方の主要モデルとの差を「ほぼ埋めた」と主張。特にエージェント型タスク・知識処理・推論で強さを示すという。Simon Willison は「フロンティアから 3〜6 か月遅れだが、価格で完全に塗り替えている」と評している。

### 圧倒的な価格

| モデル | 入力 ($/1M tokens) | 出力 ($/1M tokens) |
|--------|--------------------|--------------------|
| V4-Flash | $0.14 | $0.28 |
| V4-Pro | $1.74 | $3.48 |

Flash は OpenAI の GPT-5.4 Nano を下回り、Pro は「フロンティアクラスとして最も安い」選択肢になった。FLOPs / KV キャッシュ削減と MoE のアクティブパラメータ削減が、この価格設定を裏付けている。

### オープンソース戦略の継続

V3 / R1 で示した「オープンウェイト + 低価格 API」というパターンを V4 でも踏襲。米国系プロプライエタリの集中度が増す中で、企業が自前ホスティング・微調整・データ流出リスク回避を選べる選択肢として位置づけが強まる。

## 今後の注目点

- **長文コンテキスト性能の実測**: Hybrid Attention の効果が NIAH や long-context QA で実際にどの程度出るか、独立評価待ち。
- **エージェント / ツール利用の実用度**: V3.2 でネイティブ tool-use を入れたが、V4 のエージェント性能が Claude / GPT 系と並ぶかは未検証。
- **米国の規制動向**: Stargate 関連の地政学リスクが顕在化する中、中国モデルのオープン公開に対する米国側の規制強化の有無。
- **GLM-5.1 / Qwen 系との競争**: 中国国内オープンモデル間の競争が「規模」と「効率」の両軸で激化しており、V4 が標準的に選ばれるかは導入実績次第。
- **ホスト先の選択肢**: 1.6T のオープンウェイトを動かせる推論バックエンド（vLLM / SGLang / TensorRT-LLM 等）の対応状況が、実用採用速度を左右する。
