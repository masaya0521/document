# World Models 競争の本格化 — AMI Labs $1B 調達と Yann LeCun の賭け

- **日付**: 2026-05-01
- **カテゴリ**: Tech
- **ソース**: [TechCrunch](https://techcrunch.com/2026/03/09/yann-lecuns-ami-labs-raises-1-03-billion-to-build-world-models/) / [Nature](https://www.nature.com/articles/d41586-026-00820-5) / [SiliconANGLE](https://siliconangle.com/2026/03/10/yann-lecuns-new-startup-ami-labs-raises-1-03b-train-world-models/) / [Latent.Space](https://www.latent.space/p/ainews-yann-lecuns-ami-labs-launches)

## 概要

Meta を退いた Yann LeCun（チューリング賞受賞者・元 Meta Chief AI Scientist）が共同創業した **AMI Labs** が、欧州スタートアップ史上最大級となる **$1.03B のシードラウンド**を調達した（pre-money $3.5B、post-money $4.5B）。同社のミッションは「言語ではなく現実から学ぶ AI」、すなわち **World Models（世界モデル）** の構築であり、コア技術は LeCun が長年提唱してきた **JEPA（Joint Embedding Predictive Architecture）**。

2026 年に入り Google・Nvidia・複数のスタートアップが World Models 領域へ一斉に参入し、Nature・MIT Technology Review といった主要メディアも「LLM 中心の AI の次のパラダイム」として大きく扱い始めた。AMI Labs の巨額調達は、その潮流を象徴する出来事であると同時に、欧州にも AI フロンティアの拠点が形成された点で地政学的にも意味を持つ。

## 詳細

### World Models とは何か

World Models とは、物理世界の振る舞い（物体の動き、因果関係、時空間の連続性）を内部表現として保持し、行動の結果を予測できる AI 設計を指す。LLM が「次のトークン」を予測するのに対し、World Models は「次の世界状態」を予測する。

主な用途として想定されるのは以下の領域：

- **自律ロボット / ロボタクシー**: 環境のシミュレーションを内部で行い、安全な行動選択をする
- **ドローン・物流**: 地形・気象・障害物を含む 3D 環境での経路計画
- **エネルギー・製造業**: プラントや設備の挙動予測と制御
- **科学研究**: 物理シミュレーションの加速

LeCun の長年の主張は「LLM は流暢に話せても物理を理解しない」「真の AGI には世界モデルが必要」というものであり、AMI Labs はその思想を製品レベルで実装する初のフルスタック企業となる。

### JEPA: 中核アーキテクチャ

JEPA（Joint Embedding Predictive Architecture）は LeCun が 2022 年以降 Meta で発表してきた一連の論文で具体化された手法。要点は：

- **生成ではなく予測**: 画像・動画のピクセルを再生成せず、抽象表現空間で「次の状態」を予測する
- **自己教師あり学習**: ラベルなしの動画データから、世界の規則性を抽出
- **マルチモーダル統合**: 視覚・言語・音声・センサーを共通の埋め込み空間にマップ

V-JEPA（動画版）、I-JEPA（画像版）と段階的に発表されてきた成果を、AMI Labs は商用 World Model として統合・スケールする計画。

### 経営チームと投資家

| 役割 | 人物 | 経歴 |
|------|------|------|
| Chairman | Yann LeCun | 元 Meta Chief AI Scientist、NYU 教授、Turing Award 2018 |
| CEO | Alex LeBrun | 元 Nabla（医療 AI）、過去に Wit.ai を Facebook に売却 |
| COO | Laurent Solly | 元 Meta VP for Europe |
| Chief Science Officer | Saining Xie | 元 Meta、Vision Transformer 系研究で著名 |
| Chief Research and Innovation Officer | Pascale Fung | 元 HKUST、対話システム・倫理 AI の世界的研究者 |
| VP World Models | Michael Rabbat | 元 Meta、JEPA 共同研究者 |

リード投資家は Cathay Innovation / Greycroft / Hiro Capital / HV Capital / **Bezos Expeditions（Jeff Bezos のファミリーオフィス）**。Tim & Rosemary Berners-Lee、Jim Breyer、Mark Cuban、Mark Leslie、Xavier Niel、Eric Schmidt らもエンジェルとして参加し、欧米テック界のオールスター布陣が揃った。

### 競合構図

2026 年現在、World Models / Physical AI 領域では以下のような構図ができつつある：

- **Google DeepMind**: Genie 系 / Veo 系で動画生成と世界シミュレーションを推進
- **NVIDIA**: GTC 2026 で物理 AI / Cosmos / Alpamayo（自動運転 OSS モデル）を発表、SDK 中心に展開
- **OpenAI**: Sora の延長線で物理シミュレーション能力を強化、ロボット領域に再参入
- **Meta**: LeCun 退社後も V-JEPA 系の研究は継続、ただし社内の戦略的優先度は LLM / 製品統合寄り
- **AMI Labs**: World Models に純粋特化、ロボティクス・自律機械にダイレクトに供給
- **Wayve / Skild AI / Physical Intelligence**: ロボティクス特化のスタートアップが個別領域を攻める

AMI Labs の差別化ポイントは「LLM ではなく World Models を製品アジェンダの中心に据える」純度の高さで、「AGI への別ルート」を提示している点にある。

### 欧州にとっての意味

シード $1B は欧州スタートアップ史上最大級。これまで欧州は AI フロンティアでは米中に後塵を拝してきたが、

- Mistral（パリ）— LLM
- AMI Labs（パリ）— World Models
- Black Forest Labs（独）— 画像生成
- Stability の後継プロジェクト群

など、各セグメントで欧州拠点の有力プレイヤーが揃ってきた。EU AI Act 下での規制環境を活かしつつ、米国型の競争に対抗できる規模の研究開発体制が初めて立ち上がった象徴的事例といえる。

## 今後の注目点

- **マイルストーン**: 最初のデモ（公開 World Model API か、ロボティクス向け SDK か）の時期と質。LeCun は「数年単位」のタイムラインを示唆。
- **データ戦略**: 動画・センサーデータの大規模収集をどう行うか。Meta 時代の YouTube / Instagram スケールには届かず、提携・パートナー戦略が鍵。
- **計算資源**: $1B シードは計算インフラ投資の前段。Hyperscaler との提携（AWS Trainium、GCP TPU、Azure ND シリーズ）か、自社データセンター構築かの選択が次の焦点。
- **ロボティクス顧客**: Boston Dynamics・Figure・Apptronik・自動車 OEM 等との商用提携が成立するか。
- **JEPA の論文 → 製品ギャップ**: 学術成果を製品レベルにスケールできるか、技術的検証が必要。
- **LLM との統合**: World Models は「LLM の代替」ではなく「LLM の補完」となる可能性が高く、両者を組み合わせるアーキテクチャの設計が業界全体の課題に。
- **規制・倫理**: 物理世界に作用する AI の責任設計は LLM より深刻で、EU AI Act の高リスク用途規制との整合性が試金石となる。
