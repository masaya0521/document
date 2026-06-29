# AI コンピュート争奪戦 — 自社チップと地政学

- **日付**: 2026-06-30
- **カテゴリ**: Tech
- **ソース**: [OpenAI](https://openai.com/index/openai-broadcom-jalapeno-inference-chip/) / [Tech Startups](https://techstartups.com/2026/06/29/top-tech-news-today-june-29-2026/) / [Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/broadcom-and-openai-unveil-custom-built-jalapeno-inference-processor-openais-first-chip-is-a-massive-reticle-sized-asic-built-in-an-ultra-fast-nine-month-development-cycle)

## 概要

2026年6月末、AI 業界の主導権争いの焦点が「最良のモデルを作れるか」から「推論を回すための計算資源（コンピュート）を確保・最適化できるか」へと明確にシフトした。同じ週に、OpenAI が初の自社設計 AI チップ「Jalapeño」を発表し、Google が計算資源不足を理由に Meta への Gemini 提供を制限し、韓国が国家規模の半導体・AI 投資計画を打ち出した。これらは独立した出来事に見えて、いずれも「コンピュートが戦略インフラ・地政学的パワーになった」という同じ構造を映している。

## 詳細

### OpenAI の垂直統合 — Jalapeño

OpenAI は Broadcom・Celestica と組み、LLM 推論専用 ASIC「Jalapeño」を公開した。特徴は以下の通り。

- **推論特化**: 学習用アクセラレータの転用でも汎用 AI プロセッサでもなく、LLM の挙動理解に基づき、データ移動コスト・compute と memory のバランス・ネットワーク効率といった「推論時の実ボトルネック」を狙って設計された専用 ASIC。
- **異例の開発速度**: 初期設計からテープアウトまで約9か月。高性能先端半導体としては「史上最速級の ASIC 開発サイクル」と謳われる。レチクルサイズの巨大 ASIC。
- **電力効率**: 初期テストで現行 SOTA を大幅に上回る性能/ワットを示し、ラボでは GPT-5.3-Codex-Spark を含む実ワークロードを本番想定の周波数・電力で実行中。
- **展開**: 多世代コンピュートプラットフォームの第一歩で、2026年末から Microsoft 等のギガワット級データセンターで展開予定。

NVIDIA GPU への依存度を下げ、推論コストの構造を自社で握ろうとする「垂直統合」の動きであり、Google（TPU）・Amazon（Trainium/Inferentia）に続くハイパースケーラー型の内製化路線にフロンティアラボが本格参入したことを意味する。

### Google が Meta の Gemini 利用を制限

Google は Meta が要求した計算能力を供給しきれず、3月頃から Gemini モデルの提供を制限した。これにより Meta の社内 AI プロジェクトの一部が遅延。Google はその後ほかの顧客にも制限を広げ、さらに Elon Musk の SpaceX からクラウド計算能力を追加で借りる契約を結んだと報じられた。「計算資源の供給者が、競合にもなり得る顧客への供給を絞る」「供給者ですら外部から容量を借りる」という、需給逼迫の象徴的な構図である。

### 韓国の国家戦略

韓国は Samsung・SK Hynix を軸に、新規ファブ・HBM 増産・AI データセンター・ロボティクスを含む大規模投資計画を発表した。Samsung は HBM4 で10億ドルの売上に到達し、今後10年で約6,470億ドル規模の投資を計画。Micron も過去最高益で時価総額が Meta を超えるなど、メモリ／半導体が AI バリューチェーンの最上流の勝者として再評価されている。

## 今後の注目点

- Jalapeño が本番投入された際の実効性能/ワットと、NVIDIA GPU からの置き換え範囲（推論のどこまでを自社チップで賄えるか）。
- Google の供給制限が DMA 等の競争法・独占規制とどう絡むか。「計算資源の囲い込み」が新たな反トラスト論点になる可能性。
- HBM4 世代の供給を Samsung・SK Hynix・Micron がどう分け合うか。メモリ供給が AI 全体のボトルネックになり続けるか。
- フロンティアラボの内製チップ競争（OpenAI / Anthropic / Meta）が、Broadcom・台湾 TSMC 等の受託側の勢力図に与える影響。
