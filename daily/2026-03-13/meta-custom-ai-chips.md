# Meta カスタムAIチップ戦略

- **日付**: 2026-03-13
- **カテゴリ**: Tech
- **ソース**: [Meta公式ブログ](https://about.fb.com/news/2026/03/expanding-metas-custom-silicon-to-power-our-ai-workloads/), [CNBC](https://www.cnbc.com/2026/03/11/meta-ai-mtia-chip-data-center.html), [Tom's Hardware](https://www.tomshardware.com/tech-industry/semiconductors/meta-reveals-four-new-mtia-chips-built-for-ai-inference)

## 概要

Metaが自社設計AIチップ「MTIA（Meta Training and Inference Accelerator）」の4世代ロードマップを発表した。RISC-Vアーキテクチャベースで、TSMC製造・Broadcom協力のもと、2027年末までに6ヶ月ごとに新チップを投入する。推薦・広告システムから生成AIワークロードまで、Nvidia依存からの脱却を図る戦略的な取り組みである。

## 詳細

### チップロードマップ

| 世代 | 用途 | 特徴 | デプロイ時期 |
|------|------|------|-------------|
| MTIA 300 | ランキング・推薦 | 1コンピュートチップレット + 2ネットワークチップレット + HBM。RISC-Vベクトルコアのペアで構成 | デプロイ済み |
| MTIA 400 | R&R + 生成AI | 2コンピュートチップレット。「主要商用製品と競争力のある生パフォーマンス」を実現 | 2026年後半 |
| MTIA 450 | 生成AI推論特化 | MTIA 400の2倍のHBM帯域幅。「既存の主要商用製品をはるかに上回る」性能 | 2027年初頭 |
| MTIA 500 | 高効率生成AI推論 | MTIA 450比50%増のHBM帯域幅。2x2コンピュートチップレット構成 | 2027年 |

### アーキテクチャの特徴

- **RISC-Vベース**: オープンソースのRISC-V命令セットアーキテクチャを採用。各PE（Processing Element）にRISC-Vベクトルコアのペアを搭載
- **モジュラーチップレット設計**: コンピュート・ネットワーキング・I/Oの各チップレットを再利用可能なモジュールとして設計。個々のコンポーネントを独立して改良可能
- **冗長PE設計**: 歩留まり向上のため、冗長なPEをグリッドに配置

### 性能の進化

MTIA 300からMTIA 500にかけて、HBM帯域幅は4.5倍、コンピュートFLOPSは25倍に向上する。

### Nvidia大型契約との関係

注目すべきは、この発表がNvidiaおよびAMDとの大型調達契約の数週間後に行われた点である。Metaは短期的にはNvidiaのGPUに依存しつつ、中長期的には自社チップへの移行を進めるハイブリッド戦略を取っている。

### 業界のトレンド

Google（TPU）、Amazon（Trainium/Inferentia）、Microsoft（Maia）に続き、Metaもカスタムシリコン開発に本格参入。大手テック企業によるAI推論ワークロードの内製化トレンドが加速している。

## 今後の注目点

- MTIA 400の実デプロイ時のベンチマーク結果とNvidia H100/B200との比較
- 生成AI推論コストの削減効果がMeta全体の収益にどの程度影響するか
- RISC-Vベースのアプローチが他社の設計選択に与える影響
- 来週のNVIDIA GTC 2026でのNvidia側の対抗戦略
- 6ヶ月サイクルの新チップ投入が実際に維持可能かどうか
