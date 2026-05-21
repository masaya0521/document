# Anthropic × SpaceX Colossus 巨額契約が描く AI インフラの新地形

- **日付**: 2026-05-22
- **カテゴリ**: Tech
- **ソース**: [Axios](https://www.axios.com/2026/05/20/anthropic-spacex-compute) / [TechCrunch](https://techcrunch.com/2026/05/20/anthropic-will-pay-xai-1-25-billion-per-month-for-compute/) / [Let's Data Science](https://letsdatascience.com/news/anthropic-signs-125b-per-month-colossus-compute-deal-c892b829)

## 概要

Anthropic は SpaceX に対して **月額 $1.25B（年間 $15B、2029 年 5 月まで通算 $40B 超）** を支払う巨額コンピュート契約を締結した。対象は xAI が Memphis に保有する Colossus 1 データセンター（300 MW 超、NVIDIA H100/H200/GB200 を 22 万 GPU 以上収容）で、Anthropic が同施設をフル利用する一方、xAI は自社の学習ワークロードを新設の Colossus 2 へ移行する。同社の Q2 売上見通し $10.9B との符合では、年 $15B のコンピュート支出は売上の 1.5 倍規模に達する。

## 詳細

### 契約の構造

- **支払先**: SpaceX（xAI ではなく）— Musk グループ内の資金集約構造が背景
- **対象施設**: Colossus 1（Memphis, TN）。電力 300 MW 超、220k+ GPU
- **用途**: Tom Brown（Anthropic compute chief）によれば**主に推論**用途
- **期間**: 2026 年 5 月〜2029 年 5 月の 3 年契約、90 日前通知で双方解約可能
- **ランプアップ**: 5 月・6 月は減額、後段で月額 $1.25B に到達

### なぜ「Anthropic が Musk のインフラ」を選んだのか

Anthropic は Amazon（Trainium）と Google（TPU）と既に深い提携を持つ。にもかかわらず Musk グループから推論キャパシティを買う判断は以下で説明できる:

1. **量的逼迫**: AWS Trainium3 / Google TPU v6 でも、Claude 4.X 系の推論需要を捌ききれない実態
2. **電力の即応性**: Colossus 1 は既に 300 MW を稼働中で、新設データセンタの 18-24 か月待ちを回避できる
3. **NVIDIA GPU 互換性**: H100/H200/GB200 環境で動く既存推論スタックを移植コスト最小で展開可能
4. **政治的ヘッジ**: 単一クラウドへの依存リスクを分散し、Trump 政権下で Musk 系を完全に外せないという現実認識

### xAI 側のロジック

xAI は Colossus 1 を Anthropic に貸し出すことで、学習用 Colossus 2（新型 GPU・水冷・高密度）への投資原資を確保する。短期的には自社学習能力を一部犠牲にしてでも $40B 超の安定収入を取りに行く判断で、これは xAI の評価額／IPO 観測に直結する。Musk グループ全体の AI インフラを「学習＝Colossus 2／推論＝Colossus 1」と機能分割する戦略でもある。

### マクロ的含意

- **Anthropic の黒字化軌道**: Q2 は初の四半期黒字化見込みだが、年 $15B のインフラ支出を吸収するには売上 $30-40B 水準への到達が必須
- **AI インフラの「賃貸化」加速**: 自前データセンタを持たないモデルプロバイダが、xAI/Oracle/CoreWeave などから長期 PPA 的に GPU を借りる構造が定着
- **政治と技術の交差**: Musk と Anthropic CEO Dario Amodei の AI 安全観は対立的だが、商業契約は別軸で進む現実

## 今後の注目点

- **解約条項の発動有無**: 90 日通知での解約が「キャンセル料なし」なら、AI 需要急変時のリスク管理として重要
- **Colossus 2 の稼働開始時期**: xAI 自身の学習能力が一時的に低下する期間
- **NVIDIA の集中度**: 単一施設に H100/H200/GB200 が 22 万基集中することのレジリエンス・電力リスク
- **競合の動き**: OpenAI（Microsoft・SoftBank Stargate）／Google（TPU 自社）／Meta（自社）が同様の長期コンピュート契約に動くか
- **会計処理**: $40B+ コンピュート負債が Anthropic のバランスシートと評価額に与える影響
