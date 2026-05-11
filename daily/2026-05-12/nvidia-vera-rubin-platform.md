# NVIDIA Vera Rubin プラットフォーム — エージェント AI 時代のインフラ

- **日付**: 2026-05-12
- **カテゴリ**: Tech
- **ソース**: [NVIDIA Newsroom — Vera Rubin Platform](https://nvidianews.nvidia.com/news/nvidia-vera-rubin-platform), [NVIDIA Newsroom — Rubin Six New Chips](https://nvidianews.nvidia.com/news/rubin-platform-ai-supercomputer)

## 概要

NVIDIA が Blackwell の次世代となる「Vera Rubin」プラットフォームを正式に全面生産入りさせた。Rubin は単なる GPU 世代交代ではなく、エージェント AI（自律的にタスクを遂行する AI）のスケールアウトを前提に設計された「AI ファクトリー」プラットフォームであり、6 〜 7 種類の専用チップを 1 つのシステムに統合する点が特徴である。AWS、Google Cloud、Microsoft Azure、OCI が 2026 年後半から Rubin インスタンスを順次提供する見込みで、ビッグテック 4 社の AI 設備投資 7,250 億ドルの主要な投資先となる。

## 詳細

### Rubin プラットフォームの構成

NVIDIA が公開した Rubin プラットフォームには以下のコンポーネントが含まれる。

- **Vera CPU**: Grace の後継となる Arm ベース CPU。
- **Rubin GPU**: HBM4 を採用した次世代 GPU。
- **Rubin Ultra GPU**: より大容量・高帯域の上位 SKU。
- **NVLink Switch 6**: ラック内インターコネクト。
- **CX-9 SuperNIC**: 800Gbps 級スマート NIC。
- **Quantum-X800 InfiniBand / Spectrum-X イーサネット**: ファブリック層。

これらを 1 つのアーキテクチャに束ねることで、データセンター 1 棟がそのまま「1 つの巨大なコンピュータ」として動作するように設計されている。NVIDIA は Rubin と Blackwell を合わせた 2 世代で 2026〜2027 年に 1 兆ドルの売上を見込むとしている。

### Blackwell からの飛躍

Blackwell（B200／GB200）はトレーニングと推論の両方をターゲットにした世代だったのに対し、Rubin はエージェント AI のワークロード（多段ツール呼び出し、長時間の思考、外部 API へのアクセス）を前提とした設計が随所に見られる。

- **メモリ帯域**: HBM4 採用により Blackwell 比で大幅向上。エージェントの長コンテキスト推論で支配的になりやすいメモリボトルネックを緩和。
- **インターコネクト**: NVLink Switch 6 と CX-9 SuperNIC により、ラックを跨ぐ大規模モデル分散実行が低レイテンシで可能。
- **電力効率**: 1 ドル投資あたりの推論性能で Blackwell 比 80% 改善（NVIDIA 自社ベンチマーク）。

### クラウド事業者の動き

NVIDIA は AWS、Google Cloud、Microsoft、OCI が「2026 年後半に Rubin ベースのインスタンスを最初に提供する」と明言した。一方で同日付けの記事によれば、Google は自社の TPU 8t / 8i を Cloud Next 2026 で発表しており、ハイパースケーラーは Rubin に依存しつつも自社シリコンへのシフトも並行進行させている。

### コーニングとの 32 億ドル光ファイバー提携

NVIDIA は同時期に、コーニングと組んで光ファイバーの新工場 3 拠点（ノースカロライナ州・テキサス州）への投資を発表した。投資総額は最大 32 億ドル、3,000 人以上の雇用を生み、コーニングの米国内光学製造能力を 10 倍にスケールする計画である。これは Rubin プラットフォームのファブリック層（NVLink / InfiniBand）のスケールアウトを米国内サプライチェーンで担保する戦略的投資といえる。

### 競合状況

同じ週、CNBC は「ウォール街の AI チップ愛は NVIDIA から Intel、AMD、Micron に移りつつある」と報じた。AMD MI400 シリーズ、Intel Gaudi 4、そして Google TPU 8t / 8i といった対抗馬が出揃ったことで、NVIDIA のシェア独占が崩れる可能性が指摘されている。Rubin の全面生産入りは、こうしたシェア低下懸念への回答でもある。

## 今後の注目点

- **5/20 の決算発表**: 2027 年度第 1 四半期決算。Blackwell の出荷ペース、Rubin の最初のキャパシティ予約、データセンター粗利率の動きを確認したい。
- **クラウド各社の Rubin デプロイ時期**: AWS / Azure / GCP / OCI が後半「いつ」一般提供するかで、AI スタートアップの推論コストが大きく変動する。
- **エネルギー制約**: 7,250 億ドル投資のボトルネックは半導体ではなく電力。データセンター電力契約、原子力 SMR、再エネ PPA の動向が AI 投資ペースを左右する。
- **エージェント AI ワークロードのベンチマーク標準化**: Terminal-Bench 2.0 のようなエージェント評価が業界標準となるか、それに対し Rubin がどう優位を示せるか。
- **米国製造回帰の規制／補助金**: CHIPS Act 第 2 弾、関税、輸出規制が NVIDIA の設備投資戦略に与える影響。
