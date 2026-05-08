# Anthropic × xAI/SpaceX Colossus コンピュート提携

- **日付**: 2026-05-09（提携発表は 2026-05-06）
- **カテゴリ**: Tech
- **主要ソース**: [Anthropic 公式](https://www.anthropic.com/news/higher-limits-spacex) / [xAI 公式](https://x.ai/news/anthropic-compute-partnership) / [CNBC](https://www.cnbc.com/2026/05/06/anthropic-spacex-data-center-capacity.html) / [Bloomberg](https://www.bloomberg.com/news/articles/2026-05-06/anthropic-inks-computing-deal-with-spacex-to-meet-ai-demand) / [Simon Willison](https://simonwillison.net/2026/May/7/xai-anthropic/)

## 概要

Anthropic は xAI が運用する Memphis の AI スーパーコンピュータ「Colossus 1」のコンピュート容量を、SpaceX を経由するスキームで購入する契約を 2026-05-06 に発表した。300MW 超を1か月以内に確保し、Claude Code Pro/Max/Team のレートリミットを倍増、API のレートリミットも大幅引き上げを即時実施した。さらに Anthropic は SpaceX との「ギガワット級の宇宙コンピュート」共同開発にも興味を表明し、AIインフラの境界がオービタルへ拡張する兆しを示した。

Anthropic が Q1 2026 に約80倍の利用増を経験し Claude Pro/Max の品質劣化を引き起こしていた背景を考えると、本契約は短期的な可用性回復策であると同時に、Amazon・Google・Broadcom・Microsoft・NVIDIA・Fluidstack に並ぶ7社目の戦略的供給契約として、ハイパースケーラ依存のリスク分散にも寄与する。

## 詳細

### 契約スキームと容量

- 提供基盤は xAI の Colossus 1（Memphis、220k+ NVIDIA GPU）。Bloomberg/CNBC によれば SpaceX が中間レイヤとなり、xAI のキャパシティを Anthropic に再販する複層構造。
- 即時容量は 300MW 超、1か月以内に投入完了予定。Anthropic 側のリリースは「Claude Opus 系の API レートリミットを considerable に拡大」と表現。
- Claude Code は5時間あたりレートを倍増、Pro/Max のピーク時間帯ペナルティを撤廃。

### "ライバルが供給者に" の構図

- Elon Musk 率いる xAI は Anthropic の競合だが、Colossus 1 のキャパシティはモデル開発側よりサービス側で枯渇しがちで、xAI にとっては余剰容量の収益化、Anthropic にとってはマルチクラウドの選択肢拡大、双方にメリットが立つ。
- Simon Willison の分析では、Anthropic がこれだけの容量を「外部の単一プロバイダ」から取れることが、AIインフラの市場流動性が想定より高いことの証左と位置付けている。

### 宇宙コンピュートへの言及

- 共同声明には「ギガワット級の orbital compute infrastructure を SpaceX と探索する」とあり、放熱・電力・低レイテンシの物理制約をデータセンター屋外設置や軌道上設置で解こうとする動きが顕在化。Panthalassa の floating data center（5/8 に Peter Thiel から 1.4億ドル調達、評価額10億ドル前後）と並び、AIインフラの「物理革新」がレースのテーマになりつつある。

### 競争環境と意味合い

- Anthropic はこれで Amazon（Trainium含む）/Google（TPU）/Broadcom/Microsoft/NVIDIA/Fluidstack/SpaceX(xAI) の少なくとも7プロバイダから容量を確保するマルチソーシング戦略となり、ハイパースケーラの単一障害点リスクを構造的に低減。
- 一方で xAI 側は「自社モデル学習に使うはずの Colossus 1 キャパを売る」格好になっており、xAI の Grok 開発進捗・Colossus 2 投入時期次第では再び需給が逼迫するリスクがある。

## 今後の注目点

- xAI Colossus 2 の立ち上がり時期と、Anthropic の Q2/Q3 にかけての Claude 4.7 / 5 系モデル投入によるトラフィック増との兼ね合い
- SpaceX 中間レイヤのオペレーション実態（電源・冷却・運用責任の分担）。AWS US-EAST-1 の冷却障害（同時期に発生）が示すように、300MW 級のラピッドキャパシティ追加には熱設計の追従が大きな課題
- 「宇宙コンピュート」の現実性と規制論点（軌道上の電磁干渉・廃棄物・放熱）。Panthalassa の海上 DC との比較で、どちらがコスト/サステナビリティで先行するか
- 米政府の AI モデル事前審査（FDA型）と、外部コンピュートを使った学習・推論への規制の波及範囲
