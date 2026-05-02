# Anthropic × Amazon の $100B / 5GW 提携と Project Rainier 稼働

- **日付**: 2026-05-02
- **カテゴリ**: Tech
- **ソース**: [About Amazon](https://www.aboutamazon.com/news/aws/aws-project-rainier-ai-trainium-chips-compute-cluster) / [Anthropic Newsroom](https://www.anthropic.com/news/anthropic-amazon-compute) / [TechCrunch](https://techcrunch.com/2026/04/24/google-to-invest-up-to-40b-in-anthropic-in-cash-and-compute/)

## 概要

AWS は 4 月末に「Project Rainier」と呼ばれるスーパーコンピュータクラスタを完全稼働させた。約 50 万基の Trainium2 チップを単一クラスタとして接続した世界最大級の AI 学習基盤で、Anthropic が Claude シリーズの学習・推論を回す主戦場となる。同時に Anthropic は AWS と総額 $100B 超・最大 5GW の長期コンピュート契約を発表し、Trainium2/3/4 と将来世代の優先購入権までを抱え込んだ。Google も別途、最大 $40B（現金＋TPU クレジット）の追加出資を表明しており、フロンティア AI 企業 1 社をハイパースケーラ 2 社が「コンピュートの両建て」で囲い込む構図が固まった。

## 詳細

### Project Rainier の規模感

- 単一の AI クラスタとして「世界最大級」と AWS が公式に位置づけた構成。Trainium2 を約 50 万基結合し、Anthropic は実利用ベースで「100 万基超の Trainium2」を学習・サービングに動員済みと表明。
- Trainium は AWS 自社設計の AI アクセラレータで、Anthropic だけでなく OpenAI、Apple もサンプリング段階で評価。NVIDIA H100/B200 / Google TPU と並ぶ「第 3 のエコシステム」を確立した形。
- 電力面では「最大 5GW」のコミットが核心。比較対象として大型原発 4〜5 基相当で、AI インフラがいまや国家規模のエネルギー消費体になっていることを示す。

### コミットメントの内訳

- Anthropic は今後 10 年で AWS テクノロジーへ $100B 超を投じる。本年（2026 年）前半に Trainium2 の追加容量、年末までに Trainium2＋Trainium3 で約 1GW 分が稼働開始予定。
- Trainium4 と「将来世代を優先購入する権利」もパッケージ化されており、Anthropic は次世代チップの先頭ロットを継続的に押さえる。
- 一方で Anthropic は Google からも最大 $40B の出資（現金＋コンピュート）を受け、TPU 利用枠も同時拡大。Broadcom とのパートナー拡張で、ASIC 領域の選択肢も広げる。

### マーケットへのインプリケーション

- Microsoft（OpenAI 経由）、Amazon（Anthropic 経由）、Google（Gemini 自社＋Anthropic 出資）の 3 軸で、AI ワークロードの**一極集中ではなく多極化**が進行。
- AWS の capex は 2026 年で $125B、Microsoft は同 $190B にまで膨張し、両者の決算で「AI 投資の収益化に時間がかかる」という懸念が再燃した（Microsoft 株は決算後 -5.3%）。
- Anthropic 側の戦略は「単一サプライヤーに縛られない」点で OpenAI（実質 Microsoft 依存）との差別化要素になる。複数のシリコン上で Claude を回せることは、価格交渉力と供給リスクヘッジの両面で効く。

## 今後の注目点

- Trainium3 のスペックと実効性能 — H100/B200 比でどこまで価格性能比を出せるか
- Anthropic の収益化ペース — $100B コミットの返済原資となる ARR がどの速度で積み上がるか
- 米中の輸出規制が Trainium 系で緩いことの戦略的意味（NVIDIA だけがボトルネックという構図の崩壊）
- BlackRock/MGX による Aligned Data Centers $40B 買収など、データセンター実物資産への PE マネー流入の継続性
- Project Rainier の電力供給契約 — 原子力 SMR や長期 PPA との連携が次の論点に
