# Anthropic の急成長と $200B Google Cloud 契約が示すもの

- **日付**: 2026-05-11
- **カテゴリ**: Tech
- **ソース**: [The Information](https://www.theinformation.com/articles/anthropic-commits-spending-200-billion-googles-cloud-chips) / [Anthropic Blog](https://www.anthropic.com/news/google-broadcom-partnership-compute) / [CNBC](https://www.cnbc.com/2026/04/24/google-to-invest-up-to-40-billion-in-anthropic-as-search-giant-spreads-its-ai-bets.html) / [Engadget](https://www.engadget.com/2165585/anthropic-reportedly-agrees-to-pay-google-200-billion-for-chips-and-cloud-access/)

## 概要

Anthropic は 4 月時点で **年換算売上（run-rate revenue）が約 $300 億**に達したと明らかにした。2025 年末時点では $90 億だったため、わずか 4 ヶ月で **3 倍以上の急成長**となる。Q1 単独で見ても売上は前年同期比 80 倍。

並行して 5 月 5 日、The Information が Anthropic と Google Cloud の **5 年間で約 $2,000 億**規模のコンピュート契約を報じた。Google 側は別途、Anthropic への最大 $400 億の投資を実行している（4 月 24 日 CNBC 報道）。Anthropic CFO Krishna Rao はこれを「最も重要なコンピュート・コミットメント」と表現している。

## 詳細

### 売上カーブの異常さ

| 時点 | Run-rate Revenue |
|------|------------------|
| 2024 年末 | 約 $10 億 |
| 2025 年末 | 約 $90 億 |
| 2026 年 4 月 | 約 $300 億 |

純粋な指数関数的成長で、SaaS 企業として歴代でも極めて稀。背景は明確で、

- Claude Code / Claude Agent SDK によるコード生成需要
- 「Claude for Financial Services」「Claude for Legal」など垂直特化エージェント
- 大企業による Claude API への正面切ったコミット（JPMorgan 等が AI を R&D からコアインフラに再分類した動きと連動）

### $200B 契約のスケール感

仮に $200B が確定すれば、

- **Alphabet の総 cloud バックログの 40% 超**を 1 社が占める計算
- Anthropic 自身が公表している 2030 年までの capex 計画の **約 40%** に相当
- 開始は **2027 年から**で、Google と Broadcom が共同開発する次世代 TPU 数ギガワット分が割り当てられる

つまり、Anthropic は AWS（Trainium 経由）、Google（TPU 経由）、SpaceX / xAI（Colossus 経由）と複数の調達ルートを並行確保しに行っている。「コンピュートの分散調達」が AI ラボの戦略の中心になりつつあることを示す。

### Google から見た構図

注目すべきは「Google が Anthropic に投資した $40B」に対して、Anthropic が Google に **5 倍の $200B を支払う**という資金循環。

- 投資家から見れば、Google は Anthropic 株式のリターン + TPU / Cloud 収益の二段重ねでアップサイドを取れる
- Anthropic から見れば、株式での資金調達 → コンピュート購入という単純構造で、レバレッジが効きやすい
- 一方、AI バブル懸念派からは「ベンダーファイナンス的循環取引ではないか」との批判が出ている

### Nvidia / OpenAI との対比

ほぼ同時期に Nvidia は累計 AI 投資が **$400 億を突破**（IREN $21 億、Corning $32 億などを上乗せ）。OpenAI も Oracle と同様の超大型契約を進行中で、AI ラボ × クラウドハイパースケーラー × チップベンダーの 3 すくみが急速に固定化している。Anthropic の動きはこの構造のなかで「Google 陣営」のポジション取りを明確化した格好。

## 今後の注目点

- **2027 年からの TPU 供給が遅延しないか**: Broadcom の次世代 TPU の歩留まりと、Google データセンターの電力 / 用地確保。
- **AWS Trainium との両天秤**: Anthropic は Amazon からも巨額調達済み（Trainium3 が 2026 年初から稼働）。比率の変化はどこで反映されるか。
- **収益化の持続性**: Run-rate $30B はあくまで「足元年率換算」。Claude Code 等のエンタープライズ契約更新サイクルが回ったときに維持できるかが本番。
- **規制リスク**: 中国が Meta の Manus 買収を阻止した動きや、米貿易裁判所の関税差し止め判決と合わせて、AI 大型ディールが地政学リスクに晒される傾向は強まっている。
- **「循環取引」批判への対応**: SEC や英 CMA、EU 競争当局が AI 大手間の資本 + コンピュート契約を「実質的な独占」として精査する流れが出ないか。
