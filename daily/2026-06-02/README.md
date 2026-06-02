# Daily Digest — 2026-06-02

## Tech News

| # | トピック | 概要 | ソース |
|---|---------|------|--------|
| 1 | NVIDIA「RTX Spark」発表 | NVIDIA が Windows on Arm 向け Grace Blackwell スーパーチップ「RTX Spark」を発表。Arm CPU 最大20コア + Blackwell GPU + 128GB 統合メモリで、ローカルで120Bパラメータ LLM 実行や 1440p ゲーミングを謳う。秋に Dell/HP/Lenovo 等から発売。 | [NVIDIA Newsroom](https://nvidianews.nvidia.com/news/nvidia-microsoft-windows-pcs-agents-rtx-spark) |
| 2 | 初の自律型 LLM エージェント侵入を観測 | Sysdig が5月10日、人間の指示なしに LLM エージェントが marimo の RCE 脆弱性（CVE-2026-39987）から4段階のピボットを経て1時間未満で PostgreSQL DB を全件流出させた事例を初めて記録。 | [Sysdig](https://www.sysdig.com/blog/ai-agent-at-the-wheel-how-an-attacker-used-llms-to-move-from-a-cve-to-an-internal-database-in-4-pivots) |
| 3 | Gemini 3.5 Flash が一般提供開始 | Google が Gemini 3.5 Flash を GA。同等モデルの4倍速、100万トークンコンテキスト、Terminal-Bench 2.1 で76.2%。価格は $1.50/$9 per 1M tokens。 | [LLM-Stats](https://llm-stats.com/llm-updates) |
| 4 | GitHub Copilot が従量課金へ移行 | 6月1日より GitHub Copilot 全プランが usage-based billing に移行。固定枠の premium request が廃止され、利用量に応じた課金体系に。 | [LLM-Stats](https://llm-stats.com/ai-news) |
| 5 | Intel「Crescent Island」データセンター GPU | Intel が Xe3P アーキテクチャ採用のデータセンター GPU を公開。HBM ではなく LPDDR5X メモリを採用し「エージェント型 AI 向けに設計」と謳う。 | [Techmeme](https://www.techmeme.com/) |
| 6 | 半導体産業、2028年に AI チップ年商1.2兆ドル予測 | SIA と Deloitte が6月1日に発表したレポートで、AI データセンター向けチップの年間売上が2028年に1.2兆ドル超（4年で約10倍）に達する可能性を指摘。2026年の半導体全体売上は9750億ドル見込み。 | [SIA](https://www.semiconductors.org/news-events/latest-news/) |
| 7 | Microsoft が Azure Linux 4.0 を発表 | Microsoft Build（6月2日）で Azure Linux 4.0 の公開プレビューと Azure Container Linux の GA を発表。クラウドネイティブから AI ネイティブへの移行を強調。 | [Microsoft Open Source Blog](https://opensource.microsoft.com/blog/2026/05/18/from-open-source-to-agentic-systems-microsoft-at-open-source-summit-north-america-2026/) |
| 8 | Microsoft Defender の脆弱性が悪用 | CISA が CVE-2026-41091 と CVE-2026-45498 を Known Exploited Vulnerabilities に追加。連邦機関に6月3日までの修正適用を要求。1週間で計3件の Microsoft 脆弱性が悪用判明。 | [The Hacker News](https://thehackernews.com/2026/05/microsoft-warns-of-two-actively.html) |
| 9 | JPMorgan が AI 投資をコアインフラに再分類 | JPMorgan Chase が AI 投資を実験的 R&D からコアインフラへ再分類。2026年技術予算は約198億ドル、AI 開発に2000人を配置。 | [CNBC](https://www.cnbc.com/technology/) |
| 10 | OpenTelemetry が GA に到達 | クラウドのテレメトリ標準となった OpenTelemetry が一般提供に到達し、AI インフラ時代へと役割を拡大。 | [The New Stack](https://thenewstack.io/opentelemetry-hits-general-availability/) |

## World News

| # | トピック | 概要 | ソース |
|---|---------|------|--------|
| 1 | 米軍がイランの拠点を爆撃 | 米軍が、イランが米軍の MQ-1 Predator 無人機を撃墜したことを受け、イランのレーダーと無人機制御施設を爆撃。中東の緊張が再び高まる。 | [NBC News](https://www.npr.org/sections/world/) |
| 2 | 株式市場、9週連続上昇で最高値更新 | Nasdaq が初の27,000超え（27,086.81）、S&P 500 も7,599.96 で最高値。テック・エネルギー株と NVIDIA の RTX Spark 発表が牽引。9週連続の上昇。 | [TheStreet](https://www.thestreet.com/stock-market-today/stock-market-today-dow-jones-sp-500-nasdaq-updates-june-01-2026) |
| 3 | 膵臓がん新薬が「前例のない」結果 | 実験的新薬 daraxonrasib が進行膵臓がん患者の生存期間を倍増。肺・大腸・卵巣がんへの応用にも期待が集まる。 | [NBC News](https://www.nbcnews.com/health/health-news/new-drugs-unprecedented-results-pancreatic-cancer-doctors-look-uses-rcna346818) |
| 4 | コロンビア大統領選が決選投票へ | 犯罪厳罰派の新人 Abelardo de la Espriella が首位に立ち、Petro 政権に近い Iván Cepeda との決選投票へ。 | [Al Jazeera](https://www.aljazeera.com/news/2026/5/31/ethiopias-election-parties-coalitions-and-candidates-explained) |
| 5 | PSG が欧州CL連覇 | パリ・サンジェルマンがブダペストの決勝でアーセナルを PK 戦で破り、CL 連覇を達成。エッフェル塔周辺で祝賀の一方、夜間の衝突で多数を拘束。 | [NPR](https://www.npr.org/sections/world/) |
| 6 | コンゴでブンディブギョウイルス流行 | コンゴ東部イトゥリ州を中心にブンディブギョウイルスの流行が継続。承認済みの治療法・ワクチンがない中、1000件超の疑い例を報告。 | [CBS News](https://www.cbsnews.com/news/laos-gold-miners-cave-rescue-trapped/) |
| 7 | 世界経済成長率、2026年は2.7%予測 | 国連が2026年の世界経済成長率を2.7%と予測（2025年は2.8%）。貿易の弱含みと金融緩和の支えが綱引き。保護主義の拡大も継続見込み。 | [United Nations](https://www.un.org/sustainabledevelopment/blog/2026/01/press-release-wesp2026/) |
| 8 | 米雇用統計に市場が注目 | 6月の重要な雇用統計の発表を前に、債券トレーダーは米経済の堅調さを確認しようと注視。FRB の利上げ観測にも影響。 | [Yahoo Finance](https://finance.yahoo.com/markets/stocks/live/stock-market-today-monday-june-1-flat-225422503.html) |
| 9 | トランプ政権、18億ドル基金から後退 | 司法省が、18億ドルの「反兵器化」基金を差し止めた裁判所判決に従う意向を表明。ICE と国境警備の資金法案の再開を模索。 | [NBC News](https://www.nbcnews.com/politics/trump-administration/trump-administration-appears-back-18-billion-anti-weaponization-fund-r-rcna347884) |
| 10 | ラオスの洞窟で金鉱労働者2人が依然行方不明 | ラオスの洞窟で金鉱労働者2人が依然行方不明。雨が捜索を妨げ、救助活動が難航。 | [CBS News](https://www.cbsnews.com/news/laos-gold-miners-cave-rescue-trapped/) |

## Japan Tech News

| # | トピック | 概要 | ソース |
|---|---------|------|--------|
| 1 | 日本政府が Anthropic「Claude Mythos」アクセス取得へ | 片山さつき金融相が、サイバー攻撃能力に長けた最新AI「Claude Mythos」の政府提供を月内に受けると表明。米政権は提供拡大に反対する中、3メガバンクも利用権取得を進める。OpenAI もサイバーセキュリティ強化モデルを政府・一部企業に提供予定。 | [日本経済新聞](https://www.nikkei.com/article/DGXZQOGN010030R00C26A5000000/) |
| 2 | 経産省、半導体・AI予算を約4倍の1.23兆円へ | 経産省が2026年度予算で全体を約50%増の約3.07兆円に拡大。目玉は半導体・AI向けの約1.23兆円で、前年の約4倍。国産先端半導体と生成AI基盤への重点投資を鮮明に。 | [eeNews Europe](https://www.eenewseurope.com/en/meti-budget-hike-japan-chip-ai-fy-2026/) |
| 3 | ラピダス、2nm補助金6315億円承認・富士通から受託 | 経産省がラピダスの2026年度技術開発補助金6315億円を承認。富士通から先端AI半導体の生産を受託し、2027年度後半の2nm量産開始へ国産体制を強化。 | [Bloomberg](https://www.bloomberg.com/jp/news/articles/2026-04-11/TD7GL7T9NJLW00) |
| 4 | スカパーJSAT、Amazon Leo と衛星通信契約 | スカパーJSATが5月28日、Amazon の低軌道衛星通信サービス「Amazon Leo」に関する契約を締結。衛星ブロードバンド領域での連携を進める。 | [日経クロステック](https://xtech.nikkei.com/news/) |
| 5 | デジタル庁、ガバメントAI「源内」大規模実証を開始 | デジタル庁が5月28日、全府省庁の約18万人の政府職員を対象にガバメントAI「源内」の大規模実証を開始。行政職員が業務で生成AIを安全に活用する基盤を整備。 | [デジタル庁](https://www.digital.go.jp/news) |
| 6 | KDDI・ドコモ、ミリ波共用中継器を実証へ | KDDIとNTTドコモが5月27日、ミリ波エリア拡大に向けた共用中継器の実証実験を上野恩賜公園で2026年夏に開始すると発表。競合間でのインフラ共用を模索。 | [日経クロステック](https://xtech.nikkei.com/news/) |
| 7 | Sakana AI、社会実装フェーズへ | 日本発AIスタートアップ Sakana AI が Google との提携や防衛装備庁の委託研究契約を通じ、研究開発に加え社会実装の領域へ踏み込む。国産フロンティアAIの育成が進む。 | [選挙ドットコム](https://go2senkyo.com/seijika/166293/posts/1352810) |
| 8 | IPA「情報セキュリティ10大脅威 2026」公開 | IPA が5月21日に「情報セキュリティ10大脅威 2026 [個人編]」ハンドブックと対策マッピングシートを公開。ランサムウェアやサプライチェーン起点の波及型インシデントへの警戒を呼びかけ。 | [IPA](https://www.ipa.go.jp/security/10threats/10threats2026.html) |
| 9 | 2026年5月の Microsoft セキュリティ更新で注意喚起 | JPCERT/CC が5月の Microsoft 製品脆弱性を修正する更新プログラムへの注意喚起を発出。悪用された場合リモートから任意コード実行の恐れ。国内でもランサムウェア被害が継続。 | [JPCERT/CC](https://www.jpcert.or.jp/at/2026/at260012.html) |
| 10 | 日立が Lenovo TruScale DaaS 採用 | レノボ・ジャパンが5月28日、日立製作所が DaaS サービス「Lenovo TruScale DaaS」を採用すると発表。東北大などは蛍光の明るさと寿命で検出する光学式湿度センサー材料を開発。 | [日経クロステック](https://xtech.nikkei.com/news/) |

## Japan General News

| # | トピック | 概要 | ソース |
|---|---------|------|--------|
| 1 | 台風6号が九州〜関東に接近、暴風警戒 | 台風6号は奄美付近を北上中で、2日夜にかけ九州南部にかなり接近。3日には本州南岸を東進し四国〜関東に接近の恐れ。太平洋側を中心に大雨と暴風に警戒。 | [tenki.jp](https://tenki.jp/forecaster/t_yoshida/2026/06/02/39146.html) |
| 2 | ソフトバンクGがトヨタ抜き時価総額首位 | SBG株が1日に前週末比15%高となり時価総額が一時49兆円超でトヨタを上回り国内首位に。約22年ぶりの首位交代。最大750億ユーロ（約14兆円）の仏投資発表も株価を押し上げた。 | [ITmedia](https://www.itmedia.co.jp/news/articles/2606/01/news072.html) |
| 3 | 日経平均、初の6万7000円台 | AI関連の「スター銘柄」が市場を席巻し、日経平均が初めて6万7000円台に到達。半導体・ハイテク株の上昇が相場を牽引。 | [日本経済新聞](https://www.nikkei.com/marketdata/quote/NK225/) |
| 4 | 高市内閣、補正予算で電気・ガス料金支援 | 高市首相が中東情勢を踏まえた補正予算について会見。7〜9月に電気・ガス料金支援を実施し、7月は電気1kWh当たり3.5円を支援する方針。 | [首相官邸](https://www.kantei.go.jp/jp/105/statement/2026/0525kaiken.html) |
| 5 | 高市内閣支持率66%、若年層で高水準 | 日経新聞の5月29〜31日調査で高市内閣支持率は66%と高水準。特に20〜40代の支持が厚く、政権運営の安定要因に。 | [日本経済新聞](https://www.nikkei.com/politics/) |
| 6 | ドル円160円攻防、日銀6月利上げ観測強まる | 中東情勢を背景に円安圧力が高まり、ドル円は160円の攻防に。6月会合での日銀利上げ確率は約66%、7月までで約90%との見方。為替介入の現実味も増す。 | [IG](https://www.ig.com/jp/news-and-trade-ideas/jpy-stays-weak-even-after-boj-show-off-hawkish-messages-260428) |
| 7 | 2026年度GDP見通し0.5%へ下方修正、CPIは上方修正 | 日銀展望リポートはイラン情勢の影響で2026年度実質GDP成長率を0.5%へ下方修正（1月時点1.0%）。一方、原油高でコアCPI見通しは1.9%から2.8%へ上方修正。 | [三菱UFJ銀行](https://www.bk.mufg.jp/report/hconwnew/F.pdf) |
| 8 | 4月有効求人倍率1.18倍で横ばい | 4月の有効求人倍率は前月比横ばいの1.18倍。雇用情勢は底堅さを維持しつつも頭打ち感も。 | [日刊工業新聞](https://www.nikkan.co.jp/spaces/view/0087305) |
| 9 | 政府、2026年版ものづくり白書を閣議決定 | 政府が2026年版ものづくり白書を閣議決定。製造業のDX・人材・サプライチェーン強靱化の課題を整理。 | [日刊工業新聞](https://www.nikkan.co.jp/spaces/view/0087305) |
| 10 | 大阪IR、夢洲で建設進む | 大阪・夢洲で日本初のカジノを含む統合型リゾート（IR）の建設が進行。2030年秋の開業に向け基礎・掘削工事が中心の段階。万博レガシーの活用も本格化。 | [日本経済新聞](https://www.nikkei.com/article/DGXZQOUF032I40T00C25A6000000/) |

## Deep Dive

- [NVIDIA RTX Spark — Windows on Arm への本格参入](./nvidia-rtx-spark.md)
- [初の自律型 LLM エージェント侵入 — AI vs AI 時代のサイバー攻防](./first-autonomous-llm-agent-intrusion.md)
- [日本政府が Anthropic「Claude Mythos」を求める理由 — AI セキュリティ主権の攻防](./jp-anthropic-claude-mythos-government.md)
- [ソフトバンクGがトヨタを抜き時価総額首位 — 22年ぶり交代が映す日本市場の構造変化](./jp-softbank-overtakes-toyota-market-cap.md)
