# NVIDIA Rubin プラットフォーム — Blackwell の次に来るもの

- **日付**: 2026-04-21
- **カテゴリ**: Tech
- **ソース**: [NVIDIA Newsroom](https://nvidianews.nvidia.com/news/rubin-platform-ai-supercomputer) / [NVIDIA Investor Relations](https://investor.nvidia.com/news/press-release-details/2026/NVIDIA-Kicks-Off-the-Next-Generation-of-AI--With-Rubin--Six-New-Chips-One-Incredible-AI-Supercomputer/default.aspx)

## 概要

NVIDIA は 4 月、Blackwell の後継となる「Rubin」プラットフォームを正式発表した。Rubin は単なる GPU 世代交代ではなく、Vera CPU・Rubin GPU・NVLink 6・ConnectX-9・BlueField-4・Spectrum-6 の 6 チップを統合した「AI スーパーコンピュータ」一式として提供される点が特徴。Blackwell 比で推論トークンコストを最大 10 分の 1、MoE モデル学習時の GPU 数を 4 分の 1 に圧縮する。供給は 2026 年下期にパートナー経由で開始される予定。

## 詳細

### 6 チップ構成

| チップ | 主要仕様 |
|--------|----------|
| Vera CPU | 88 コアのカスタム Olympus、Armv9.2 互換、NVLink-C2C で Rubin GPU と密結合 |
| Rubin GPU | 第 3 世代 Transformer Engine、50 PFLOPS の NVFP4 演算 |
| NVLink 6 Switch | GPU あたり 3.6 TB/s、ラック内で 260 TB/s |
| ConnectX-9 SuperNIC | Rubin 対応の次世代スケールアウト NIC |
| BlueField-4 DPU | ストレージ・AI 推論コンテキスト管理を担う DPU |
| Spectrum-6 Ethernet Switch | 200G SerDes、Spectrum-X で電力効率 5 倍・信頼性 10 倍 |

### Blackwell 比での性能指標

- 推論トークンコストを最大 **10 倍削減**。
- MoE モデル学習時に必要な GPU 数を **4 分の 1** に削減。
- Vera Rubin NVL72 ラックで **260 TB/s の総帯域幅**。NVIDIA は「インターネット全体より広い帯域」と表現。

### 供給・主要顧客

- 2026 年下期に AWS / Google Cloud / Microsoft Azure / Oracle Cloud / CoreWeave が採用開始。
- AI ラボ系では OpenAI / Anthropic / Meta / xAI、ODM/OEM では Dell / HPE / Lenovo / Supermicro が展開予定。
- 4/18 の CNBC 報道の通り 2026 年はゲーマー向け GeForce の新世代を出さない方針で、データセンター優先の配分が露骨に出ている。

### コンテキスト

- 米政府の対中輸出規制下で中国 AI 企業が規制違反の Nvidia サーバーを $92M 規模で調達していた事実が 4/10 に開示された。Rubin は輸出管理上の扱いが当初から焦点になる見込み。
- NVIDIA は並行して SiFive に出資（$3.65B 評価）し、RISC-V ベースの AI データセンター向け CPU の開発も推進。x86 以外の選択肢を手元に確保しつつある。

## 今後の注目点

- **実質効率の検証**: 「10 倍削減」は codesign 前提の理論値寄り。実利用での推論コスト削減幅が Blackwell ラインの減価償却に与える影響は、2026 下期〜2027 上期の各クラウド原価に直接響く。
- **電力制約と立地**: ラック密度・帯域がさらに跳ね上がる中、電力コスト・冷却・立地（米投資家所有ユーティリティの 5 年 $1.4T 投資はこれを見越したもの）がボトルネックになる。
- **対中輸出規制**: Rubin が輸出ライセンス対象になる閾値で設計されているか、それとも意図的に出荷制限を織り込んだ SKU を別に用意するかで、中国勢の実効アクセスが決まる。
- **NVLink Fusion / CUDA 周辺の囲い込み強化**: ConnectX-9 と BlueField-4 を通じてネットワーク・ストレージ層まで NVIDIA が標準化を握る動きは、AMD / Intel と Hyperscaler 自製チップへの対抗軸として強まる。
