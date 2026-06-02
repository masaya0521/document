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

## Deep Dive

- [NVIDIA RTX Spark — Windows on Arm への本格参入](./nvidia-rtx-spark.md)
- [初の自律型 LLM エージェント侵入 — AI vs AI 時代のサイバー攻防](./first-autonomous-llm-agent-intrusion.md)
