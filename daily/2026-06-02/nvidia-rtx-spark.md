# NVIDIA RTX Spark — Windows on Arm への本格参入

- **日付**: 2026-06-02
- **カテゴリ**: Tech
- **ソース**: [NVIDIA Newsroom](https://nvidianews.nvidia.com/news/nvidia-microsoft-windows-pcs-agents-rtx-spark), [Tom's Hardware](https://www.tomshardware.com/laptops/nvidia-unveils-rtx-spark-superchip-at-computex-2026-new-platform-promises-to-turn-windows-into-an-agentic-ai-os-with-arm-cpu-blackwell-gpu-and-128gb-unified-memory)

## 概要

NVIDIA が Computex 2026 で、Windows on Arm 向けの新しい PC プラットフォーム「RTX Spark」を発表した。Grace Blackwell 系のスーパーチップを中核に据え、Arm CPU・Blackwell GPU・大容量統合メモリを1パッケージに統合する。これまで Qualcomm が主導してきた Windows on Arm 市場に、GPU の巨人 NVIDIA が本格参入する号砲となる。Qualcomm の Windows on Arm 独占契約の失効というタイミングも追い風になっている。

PC を「エージェント型 AI を動かす OS」へと再定義する狙いがあり、Microsoft との協業でローカルでセキュアに AI エージェントを動かす仕組みを提供する点が最大の特徴だ。

## 詳細

### チップ仕様

RTX Spark は以下のスペックを持つ。

- **CPU**: 最大20コアの Arm アーキテクチャ（MediaTek と共同設計のカスタム CPU）
- **GPU**: Blackwell 世代、6,144 CUDA コア
- **メモリ**: 128GB LPDDR5X 統合メモリ、最大 300 GB/s の帯域幅

統合メモリ構成により、CPU と GPU が同一のメモリプールを共有する。これが大規模 LLM のローカル実行を可能にする鍵となっている。

### 性能の謳い文句

NVIDIA は RTX Spark で以下が可能だとアピールしている。

- 90GB 超の超大規模 3D シーンのレンダリング
- 12K 4:2:2 動画の編集
- 4K AI 動画の生成
- 最大100万トークンのコンテキストで **120B パラメータ LLM をローカル実行**（エージェント用途）
- AAA ゲームを 1440p / 100fps 超でプレイ

### デバイス形態とパートナー

ノート PC は 14〜16インチ、薄さ 14mm・重さ約1.4kg（3ポンド）の設計。一部モデルは G-SYNC 対応のタンデム OLED パネルを採用する。初期 OEM は ASUS、Dell、HP、Lenovo、Microsoft Surface、MSI で、後に Acer と GIGABYTE も続く。

### AI・ソフトウェア機能

NVIDIA と Microsoft は、パーソナルエージェントのためのネイティブ Windows 体験を共同で提供する。新しいセキュリティプリミティブと「NVIDIA OpenShell」により、エージェントをメインデバイス上でセキュアに実行できる。従来の x86 Windows アプリは、Arm ネイティブ版がなければ Microsoft の Prism エミュレータ経由で動く。開発者コミュニティでは既に Arm ネイティブ版や Prism 最適化アップデートの開発が始まっている。

### 提供時期と価格

RTX Spark 搭載のスリムノートとコンパクトデスクトップは2026年秋に発売予定。初期モデルは市場の上位（プレミアム）価格帯に位置づけられるが、具体的な MSRP や正確な出荷日は未発表。

## 今後の注目点

- **Qualcomm との競合**: Windows on Arm 市場で Qualcomm Snapdragon X 系と直接競合する。GPU 性能で差別化できるか。
- **x86 互換性**: Prism エミュレータの性能と、主要アプリの Arm ネイティブ対応の進み具合がユーザー体験を左右する。
- **ローカル AI の実用性**: 120B LLM のローカル実行が実用レベルの速度・電力効率で動くか、実機ベンチマークが待たれる。
- **Apple との対比**: 統合メモリ + Arm という構成は Apple Silicon に酷似。AI PC 市場で Apple M 系チップとどう棲み分けるか。
- **価格**: プレミアム価格帯で出る初期モデルが、どこまでメインストリームに降りてこられるか。
