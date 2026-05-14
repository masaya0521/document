# AWS Trainium3 と「クラウドベンダー OEM 化」の地殻変動

- **日付**: 2026-05-14
- **カテゴリ**: Tech
- **ソース**: [The Next Platform](https://www.nextplatform.com/cloud/2026/04/30/aws-will-be-an-oem-just-like-google-and-maybe-microsoft/5219100) / [SemiAnalysis](https://newsletter.semianalysis.com/p/aws-trainium3-deep-dive-a-potential) / [AWS Neuron Docs](https://awsdocs-neuron.readthedocs-hosted.com/en/latest/about-neuron/arch/neuron-hardware/trainium3.html) / [Network World](https://www.networkworld.com/article/4098773/aws-finally-moves-to-simplify-multicloud-operations-with-google.html)

## 概要

AWS の自社設計 AI チップ **Trainium3** が 2026 年初頭から本格出荷フェーズに入り、Trainium2 比で **価格性能 +30〜40%、エネルギー効率 +40%** を実現した。さらに重要なのは、AWS CEO Andy Jassy が Trainium ラック単位での外販（OEM 化）の可能性に言及したことだ。Google が TPU を Anthropic 等の外部に提供し、Microsoft も Maia をエンタープライズに開放する流れと合流すれば、**ハイパースケーラーが「自社チップを所有して外販するチップベンダー」化する地殻変動**が完成する。Nvidia 一極集中の AI インフラ構造が崩れる前兆である。

## 詳細

### Trainium3 のスペック

3nm プロセスで製造された AWS 初の 3nm AI チップ。

- **FP8 演算性能**: 2.52 PFLOPS / chip（Trainium2 比 2 倍）
- **メモリ容量**: 144 GB HBM3e（Trainium2 比 1.5 倍）
- **メモリ帯域**: 4.9 TB/s（Trainium2 比 1.7 倍）
- **UltraServer 構成**: 最大 144 チップで 362 FP8 PFLOPs にスケール
- **Trn3 UltraServer 対 Trn2 UltraServer**: 性能 4.4 倍、メモリ帯域 3.9 倍、ワットあたり性能 4 倍

「次世代の agentic / reasoning / video generation でのトークン経済性」を最適化する設計で、推論ワークロードのスケール期に対応するアーキテクチャに振っている。

### 出荷状況と内部需要

- 出荷は 2026 年初頭から開始済み
- **既存顧客需要でほぼフル予約**: Anthropic / 大手エンタープライズの内部使用枠で買い尽くされている
- Trn3 UltraServers は General Availability に移行済み

### Jassy の「OEM 化」発言の重み

> "On the question about Trainium and the notion of our selling racks over time, I do think that is very much a possibility. ... we have to decide how much we are going to allocate to the existing demand and customers and how much we are going to save to sell as racks."
>
> — Andy Jassy（AWS CEO）

この発言の含意は重い。AWS は元来「自社サービスとして提供する」モデルであり、ハードウェアを箱売りする戦略を取ってこなかった。だが Trainium 需要が既存顧客需要でも溢れ、かつ Google が TPU を「クラウド外」に出し始めた以上、AWS も同じ路線を取らないと**長期的にチップエコシステムが Google 寄りに偏る**リスクがある。

### 並行する 3 つの地殻変動

1. **マルチクラウド連携の解禁**
   - AWS が Google Cloud を最初の提携先としたマルチクラウド接続サービスをプレビュー（Azure も 2026 年中に参加予定）
   - 寡占 3 社が「相互運用」へ舵を切るのは前例のない動き
2. **AI 経由の収益成長率の非対称性**
   - Microsoft Azure: +40% YoY、Google Cloud: +63% YoY、AWS: +19% YoY
   - AWS は規模優位だが成長で見ると Google / Microsoft に追い込まれており、**カスタムシリコンの外販で差別化**するインセンティブが強い
3. **Nvidia 一極からの段階的脱却**
   - Anthropic は AWS Trainium と Google TPU 双方で大規模学習を実行中
   - OpenAI も独自チップ計画を継続
   - エンタープライズが「Nvidia 以外を選べる」ことを実感する局面が増えている

### エンタープライズ顧客への意味

- **価格交渉力の回復**: Nvidia 純正 H 系・B 系の供給逼迫期に、Trainium / TPU が現実的な代替に
- **ベンダーロックインの構造変化**: クラウド = アプリ層の SaaS だけでなく、**シリコン層のロックイン**も意識する必要
- **ソフトウェアスタックの選択**: AWS Neuron / Google JAX-on-TPU / CUDA の 3 系統が並立し、フレームワーク互換性層（PyTorch XLA, vLLM, OpenXLA 等）の重要性が増す

## 今後の注目点

- **AWS が実際にラックを「箱売り」開始するタイミング**: re:Invent 2026（11 月）が有力
- **Trainium のソフトウェア成熟度**: Neuron SDK が CUDA / cuDNN に追いつけるか。PyTorch XLA / OpenXLA との統合進度
- **OEM 販売時の保守責任**: クラウドベンダーがハードウェア保守のオペレーションを物理拠点に展開できるか
- **Nvidia の対抗策**: Spectrum-X / Quantum InfiniBand 周辺の「クラウドが真似しにくい層」での囲い込み、CUDA エコシステム強化
- **規制視点**: 米中対立下で AWS / Google / Microsoft が中国系企業に Trainium / TPU / Maia を販売できるかの輸出規制
- **Anthropic の AWS / Google 二股戦略**: Anthropic ARR が $30B に達した中、計算インフラの政治的バランスが Frontier Lab 全体の動きを左右
