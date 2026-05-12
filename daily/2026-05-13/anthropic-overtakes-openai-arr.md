# Anthropic ARR が OpenAI を逆転 — 30B vs 24B

- **日付**: 2026-05-13
- **カテゴリ**: Tech
- **ソース**: [VentureBeat](https://venturebeat.com/technology/anthropic-says-it-hit-a-30-billion-revenue-run-rate-after-crazy-80x-growth) / [The AI Corner](https://www.the-ai-corner.com/p/anthropic-30b-arr-passed-openai-revenue-2026) / [Nerd Level Tech](https://nerdleveltech.com/anthropic-30-billion-arr-surpasses-openai) / [Anthropic 公式](https://www.anthropic.com/news/google-broadcom-partnership-compute)

## 概要

Anthropic は 4/7 に annualized revenue run rate（ARR）が 300 億ドルを突破したと公表。2025 年末時点では約 90 億ドルだったため、わずか 4 か月で約 3 倍に拡大した計算となる。同時期の OpenAI の ARR は約 240–250 億ドルとされ、**フロンティア AI 商用化レースで初めて Anthropic が OpenAI を売上ベースで上回った**こととなる。CEO Dario Amodei は Q1 2026 で「年率換算で 80 倍成長」と表現している。

## 詳細

### 売上の内訳と成長ドライバ

- **エンタープライズ顧客の集中**: 年間 1M ドル以上を支払う顧客が、Series G 調達直後の数か月で 500 社 → 1,000 社超に倍増
- **Claude Code が単独で 2.5B+ ARR**: 2025 年 5 月 GA、6 か月で年率 10 億ドル達成。2026 年 2 月の Series G 開示時点で年率 25 億ドル、その後さらに倍増ペース
- **コーディング・エージェント市場の独占的ポジション**: Codex / Cursor / Windsurf 等競合は存在するが、エンタープライズ採用では Claude Code がデファクト化
- **API 取引の拡大**: TCS / Infosys / Cognizant 等の SI 大手は Claude / OpenAI の両方を扱うが、コーディング系ユースケースでは Claude 比率が高まっている

### OpenAI との比較

| 指標 | Anthropic | OpenAI |
|------|-----------|--------|
| ARR (2026 年 4 月時点) | $30B | $24–25B |
| 主力プロダクト構成 | Claude Code（コーディング・エージェント）中心 | ChatGPT 消費者課金 + API + エンタープライズ |
| エンタープライズ集中度 | 高（API / Claude Code 経由が支配的） | 中（消費者課金の比率が依然高い） |
| 直近の戦略提携 | Google TPU + Broadcom（3.5GW を 2027 年に） | Novo Nordisk 等の業種別深掘り、SI 6 社連携 |

注意点として、ARR は「直近月の売上 × 12」で算出されるため、エンタープライズ大口契約 1 件で大きく動く揮発性指標である。GAAP 売上でみれば OpenAI の規模はなお大きい可能性がある。

### コンピュートインフラ戦略

Anthropic は Google / Broadcom とのパートナーシップを拡張し、2027 年に **約 3.5GW の Google TPU 容量**を確保。これに加え、SpaceX / xAI の Colossus 1 スーパーコンピュータへのアクセス契約も報じられている。GPU を Nvidia 単独に依存しない多元的な調達戦略は、ARR 30B 規模を支えるコンピュート確保の合理的な手段。

### 業界へのインプリケーション

1. **コーディング・エージェント市場の経済規模が想定を超えた**: Claude Code 単独で年率 25 億ドル超は、GitHub Copilot などの先発製品をはるかに上回るペース。AI コーディング支援は「補助ツール」から「主力開発インフラ」に転換しつつある
2. **B2B AI の収益化が一気に加速**: 76% の組織が CAIO（Chief AI Officer）職を設置済み（2025 年は 26%）という調査と整合的で、購買意思決定者の地位向上が API 単価上昇に寄与
3. **モデルプロバイダ間の差別化軸が「能力」から「エンタープライズ運用」へ**: Claude のセーフティ・コンテキスト管理・エージェントツール群が、長期間の業務運用で「壊れにくい AI」として選好されている

## 今後の注目点

- OpenAI が GPT-5.5 Instant 以降のリリースサイクルで巻き返せるか
- Claude Code のエンタープライズ TCO（Total Cost of Ownership）が顕在化したとき、ARR 成長率がどう変化するか
- Google TPU 3.5GW が実際にオンライン化される 2027 年タイミングまでのコンピュート不足リスク
- 米国主導の「主要 AI モデル事前テスト」規制の運用がフロンティア各社のリリースサイクルにどう影響するか
- Anthropic IPO の可能性と、Series G 直後の評価額（180B〜200B レンジと報じられる）の継続性
- DeepSeek V4-Flash のような効率重視モデルが、エンタープライズ採用の一部を侵食するシナリオ
