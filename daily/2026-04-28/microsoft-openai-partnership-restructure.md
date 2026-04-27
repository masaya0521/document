# Microsoft-OpenAI 提携契約の再構築：独占解消・AGI 条項撤廃の意味

- **日付**: 2026-04-27 発表 (Daily Digest 2026-04-28)
- **カテゴリ**: Tech
- **主なソース**:
  - [Microsoft Blog — The next phase of the Microsoft-OpenAI partnership](https://blogs.microsoft.com/blog/2026/04/27/the-next-phase-of-the-microsoft-openai-partnership/)
  - [OpenAI — The next phase of the Microsoft OpenAI partnership](https://openai.com/index/next-phase-of-microsoft-partnership/)
  - [CNBC — OpenAI shakes up partnership with Microsoft, capping revenue share payments](https://www.cnbc.com/2026/04/27/openai-microsoft-partnership-revenue-cap.html)
  - [Bloomberg — Microsoft to Stop Sharing Revenue With Main AI Partner OpenAI](https://www.bloomberg.com/news/articles/2026-04-27/microsoft-to-stop-sharing-revenue-with-main-ai-partner-openai)
  - [The Decoder — OpenAI and Microsoft rewrite their deal: no more exclusivity, no more AGI clause](https://the-decoder.com/openai-and-microsoft-rewrite-their-deal-no-more-exclusivity-no-more-agi-clause/)

## 概要

Microsoft と OpenAI は 2026-04-27、2019 年以降続いた戦略提携契約を大幅に改定したと共同発表した。最大の変更は、Microsoft が長く保持してきた OpenAI 製品の独占販売権を放棄し、OpenAI が Amazon AWS や Google Cloud など Azure 以外のクラウドでも自社製品を提供できるようになる点である。同時に、長く議論を呼んでいた「AGI 達成時の Microsoft の対応条項 (AGI clause)」も契約から削除された。

財務面では、Microsoft が再販する OpenAI 製品に対する revenue share の支払い義務を停止する一方、OpenAI から Microsoft への revenue share 支払い (上限あり) は 2030 年まで継続する。Microsoft の OpenAI 知財ライセンスは 2032 年まで継続するが、独占ではなくなる。

## 詳細

### 1. 独占関係の終了とクラウドの分配

- これまで Microsoft は OpenAI の API・モデルを Azure 経由で独占的に再販する権利を持っていた。今回の改定で、OpenAI は **任意のクラウドプロバイダーで全製品を販売可能** となる。
- ただし、**Microsoft は引き続き「primary cloud partner」**であり、OpenAI 製品は Azure に「first」リリースされる原則は維持。Microsoft が必要なキャパシティを提供できない / 提供しないと判断した場合に限り他クラウドへ展開する建付け。
- これは、OpenAI が AWS と結んだ約 500 億ドル規模の計算インフラ契約 (TechCrunch 報道) を実質的に解除条件として位置付けるもので、両者の法的紛争を未然に回避する効果がある。

### 2. 収益シェア構造の刷新

- **Microsoft → OpenAI 方向**: Microsoft が Azure 上で OpenAI 製品を再販した場合の revenue share 支払いが廃止。Microsoft の AI コスト構造が改善する一方、Azure OpenAI Service の利幅も拡大する見通し。
- **OpenAI → Microsoft 方向**: OpenAI から Microsoft への支払いは上限付き (capped) で 2030 年まで継続。"OpenAI の技術進展とは独立" と明記され、AGI 到達などイベント駆動で支払い構造が変わらないようにロックされた。

### 3. AGI 条項の撤廃

- 旧契約には、OpenAI の理事会が AGI に到達したと宣言した場合、Microsoft が IP ライセンスを失う / 関係性を再評価する規定があった。これが今回 **完全削除**。
- AGI 到達の定義そのものが恣意的・主観的で運用困難であったことに加え、OpenAI 側が AGI 宣言を交渉カードに使うリスクも消えたことで、Microsoft の長期投資判断は安定化する。
- 一方で、Microsoft の AGI 到達時の "セーフガード" がなくなり、OpenAI がより独立した方針 (例: 競合クラウドへのフルライセンス) を取れる構造へ。

### 4. IP ライセンスの取り扱い

- Microsoft は **2032 年まで OpenAI の AI モデル IP に対するライセンス** を保持。ただし「独占ではない」点が新規。
- これにより Microsoft は引き続きモデルの基礎技術を Copilot や Azure 製品に組み込めるが、Anthropic Claude など他社モデルも自社プロダクトに統合する道が開かれる (Stocktwits 報道)。

### 5. 戦略的な含意

- **OpenAI 側**: 計算資源の確保先を多様化でき、Stargate 計画や AWS ディール、Google TPU 利用などの選択肢が広がる。エンタープライズ顧客に対し「特定クラウド非依存」の訴求が可能に。
- **Microsoft 側**: GitHub Copilot や Microsoft 365 Copilot で Anthropic Claude を本格活用しやすくなる。OpenAI への依存度を下げ、自社の MAI / Phi シリーズや内製モデルを強化する余地が拡大。
- **業界全体**: ハイパースケーラ間の AI モデル提供戦略がフラット化し、エンタープライズ顧客にとっては「マルチクラウド × マルチモデル」が現実的なデフォルトに。

## 今後の注目点

- AWS / Google Cloud 上での OpenAI 製品の正式提供開始時期と価格設定
- Microsoft の Q3 決算 (2026-04-29 予定) における AI 関連コスト・収益ガイダンスの変化
- Azure OpenAI Service と AWS Bedrock 上の OpenAI 提供で機能差分が出るか (リリース順、リージョン、SLA)
- Microsoft 365 Copilot における Anthropic Claude 統合の進展 (Stocktwits の予告どおりか)
- AGI 条項撤廃後の OpenAI 理事会のガバナンス変化、特に「公益優先」のコミットメントがどう運用されるか
- Stargate プロジェクトの資金調達・デプロイ計画の修正
- 連邦取引委員会 (FTC) や EU 競争当局の独占性レビューが終結に向かうか
