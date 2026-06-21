# NVIDIA Rubin プラットフォームと AI インフラ競争

- **日付**: 2026-06-21
- **カテゴリ**: Tech
- **ソース**: [NVIDIA Newsroom](https://nvidianews.nvidia.com/news/rubin-platform-ai-supercomputer) / [Data Center Dynamics](https://www.datacenterdynamics.com/en/news/nvidia-updates-data-center-product-roadmap-following-lpu-launch-at-gtc-2026/)

## 概要

NVIDIA は GTC 2026 で次世代 AI プラットフォーム「Rubin」を発表し、Vera CPU を含む 6 種の新チップと AI スーパーコンピュータを公開した。Blackwell 比で最大 10 倍のトークン当たり低コストを掲げ、エージェント AI・高度推論・大規模 MoE 推論の加速を狙う。AWS・Google Cloud・Microsoft・OCI といった主要クラウドが 2026 年内に Vera Rubin ベースのインスタンス展開を予定しており、AI インフラ競争の次のステージを規定する動きとなる。

## 詳細

### Rubin プラットフォームの中核

Rubin は以下 5 つの革新を統合する。

- 最新世代の **NVLink** インターコネクト
- **Transformer Engine** の新世代
- **Confidential Computing** と **RAS Engine**
- **NVIDIA Vera CPU**

これらにより、エージェント AI・高度推論・大規模 MoE モデルの推論を、Blackwell 比で最大 10 倍のトークン当たり低コストで実行できるとする。

### ネットワークとエッジ

**Spectrum-X Ethernet Photonics** が量産入り。Co-Packaged Optics（CPO）ベースの新世代スイッチングで、Vera Rubin プラットフォームのスケールアウト/スケールアクロス展開を支える。あわせて、長時間稼働エージェント向けのオープンモデル **Nemotron 3 Ultra** を 6/4 に公開した。

### 低レイテンシ推論への布石

買収した Groq 由来の **Groq 3 LPU** を 2026 年後半に投入予定。液冷の LPX ラックは 256 基の LPU、128GB のオンチップ SRAM、640 TBps のスケールアップ帯域を備え、低レイテンシ推論ワークロードに特化する。これにより NVIDIA は学習だけでなく推論レイヤまで AI スタック全層を押さえる構えを強める。

### クラウド展開

Vera Rubin ベースのインスタンスは、AWS・Google Cloud・Microsoft・OCI に加え、CoreWeave・Lambda・Nebius・Nscale といった NVIDIA Cloud Partner が 2026 年内に先行展開する見込み。

## 今後の注目点

- 「トークン当たり 10 倍低コスト」が実運用でどこまで実現するか（電力・冷却込みの TCO）
- LPU による低レイテンシ推論市場での Groq・カスタムシリコン勢との競合
- CPO（co-packaged optics）量産がデータセンターの電力・配線設計に与える影響
- 各クラウドの Vera Rubin 展開時期と、AI インフラ投資の過熱/調整の行方
