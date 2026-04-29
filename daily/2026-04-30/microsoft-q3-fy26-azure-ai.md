# Microsoft Q3 FY26 決算で見える「Azure × AI」のユニットエコノミクス

- **日付**: 2026-04-30
- **カテゴリ**: Tech
- **ソース**:
  - [CNBC — Microsoft (MSFT) Q3 earnings report 2026](https://www.cnbc.com/2026/04/29/microsoft-msft-q3-earnings-report-2026.html)
  - [Microsoft Investor Relations — FY26 Q3](https://www.microsoft.com/en-us/Investor/earnings/FY-2026-Q3/press-release-webcast)
  - [Quartz — Microsoft Q3 2026 earnings](https://qz.com/microsoft-q3-2026-earnings-cloud-ai-growth-042926)
  - [Stocktitan — MSFT Q3 2026 cloud, AI, profit surge](https://www.stocktitan.net/sec-filings/MSFT/8-k-microsoft-corp-reports-material-event-a34ff9939e6a.html)
  - [Global Data Center Hub — Q2 FY2026 capex analysis](https://www.globaldatacenterhub.com/p/microsoft-q2-fy2026-the-375b-infrastructure)

## 概要

Microsoft が 4 月 29 日に発表した FY26 Q3（1〜3 月期）決算は、ハイパースケーラーの「AI 設備投資 → 売上認識」フライホイールが本格回転に入ったことを示す内容となった。総売上 $82.9B（+18% YoY）、希薄化後 EPS $4.27（+23%）はいずれも市場予想を上回り、5 連敗していた株価の流れを変える可能性がある。

最大の論点は 2 つ。第一に **Azure 売上 +40% YoY** が市場予想（38.8〜39.3%）を上回ったこと。第二に **AI 事業の年換算ランレートが $37B（+123% YoY）** に到達したこと。同時に、コミットメント残高 (RPO) が **$627B (+99%)** に膨らんでおり、その約 45% は OpenAI 由来とされる。

## 詳細

### 売上ミックスのリバランス

| セグメント | 売上 | 成長率 |
|---|---|---|
| Microsoft Cloud (合計) | $54.5B | +29% |
| Azure & その他クラウド | （非開示）+40% | — |
| AI 事業ランレート | $37B (年換算) | +123% |
| パーソナルコンピューティング | （非開示） | -1% |

Microsoft Cloud は単体で会社売上の 6 割超を占め、Azure 単独でその大宗を握る構造になりつつある。Q2 FY26 で Azure は +38% (CC) だったため、Q3 の +40% は再加速。一方で Xbox やデバイスを含むパーソナルコンピューティング部門はマイナス成長で、コアな成長エンジンが完全にクラウド × AI へ寄ったことを意味する。

### CapEx のショートライフ偏重

Q2 FY26 時点で総 capex は $37.5B、うち約 2/3 が GPU・CPU を中心とする「短命資産」に振り向けられた。これは「需要が見えている範囲で素早く収益化する」姿勢を示すもので、長期データセンターへの投資（建屋・電源）と並行して、即時の AI 需要を捌くためのアクセラレータ調達が前面に出ている。

| 期 | キャッシュ Capex | ファイナンスリース込 | 主用途 |
|---|---|---|---|
| Q1 FY26 | （未開示） | — | 約半分が短命資産（GPU/CPU） |
| Q2 FY26 | $29.88B | $37.5B | 約 2/3 が短命資産 |
| Q3 FY26 | — | — | 商用 RPO 急増の裏付け |

このペースで投資を続ける場合、1 年あたり $150B 規模の capex が見えてくる。Meta が今期に上方修正した $125–145B、Alphabet の $175B、Amazon の約 $200B と合わせ、**ハイパースケーラー 4 社で年 $650–700B の AI インフラ投資**という異例の規模に達する。

### Commercial RPO $627B の意味

商用残高 RPO は 1 年で **+99% 増加して $627B**。これは「将来の売上として既にコミットされた需要」の指標で、約 45% を OpenAI 関連が占めるとされる。OpenAI 単独で $280B 超のコミットを Azure 経由で消費する設計と整合する。

ただし、これは「集中リスク」も意味する。OpenAI 自体の事業継続性、収益性、そして競合（Anthropic ARR $30B 突破、Google の Gemini ライン）との優位性が崩れた場合、RPO の前倒し消化または再交渉リスクが Azure 売上計上スケジュールに直結する。

### 「Azure 経由で AI を売る」モデルが定着

注目すべきは、AI ランレート $37B のうち多くが Azure 経由のインフラ売上、Microsoft 365 Copilot のサブスクリプション、そして開発者向け Foundry サービスの 3 本柱で構成される点。これは「AI = 単発 API ではなく、エンタープライズ契約 + クラウド消費に組み込まれた継続課金」というモデルが成立しつつあることを示す。

CFO Amy Hood は前四半期のガイダンスで「FY26 通期で Azure は加速、Microsoft Cloud の粗利率は AI ミックス影響で若干低下」と説明していた。Q3 の実績はこのシナリオに沿っており、「成長と粗利率トレードオフ」をマーケットがどう評価するかが今後の株価ドライバになる。

## 今後の注目点

- **OpenAI コミットメントの稼働率**: $280B 規模の RPO を実際に Azure 上で消化できるか、消費の地理・GPU 種別の偏り。
- **粗利率の方向性**: AI 売上ミックスが上がるほど短期的にはマージンが圧迫される構造。Microsoft Cloud GP マージンの推移を四半期で監視。
- **電力・データセンター制約**: Q4 FY26 以降は北米の電力供給制約が顕在化。長命資産（変電・発電・建屋）への投資シフトが進むかを確認。
- **競合のシェア奪還**: AWS が Q1 で 20% 超の成長を維持できるか、GCP が +48% を再現できるか（Q4 2025 比較）。3 社の差分が AI ワークロードの誘致状況を映す。
- **Windows / PC 事業の縮退ペース**: PC 同梱 Copilot 戦略が PC 売上に回帰するか、それとも Cloud 一本足化が加速するか。
- **規制リスク**: EU・米州の AI 関連法、Australia の SaaS 課税（メディア助成）など、ハイパースケーラーへの課税圧力。
