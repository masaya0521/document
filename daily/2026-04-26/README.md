# Daily Digest — 2026-04-26

## Tech News

| # | トピック | 概要 | ソース |
|---|---------|------|--------|
| 1 | OpenAI が GPT-5.5 をリリース | コーディング・PC操作・深いリサーチに強い新フラッグシップを ChatGPT Plus / Pro / Business / Enterprise / Codex 向けに展開。レイテンシは据え置きで使用トークンを削減し、エージェント型ワークフローで強さを発揮。 | [CNBC](https://www.cnbc.com/2026/04/23/openai-announces-latest-artificial-intelligence-model.html) |
| 2 | DeepSeek が V4 プレビューを公開 | 1.6T パラメータ（49B アクティブ）の Pro と 284B（13B）Flash の MoE 2 種を Hugging Face で OSS 公開。コンテキスト 1M、Hybrid Attention Architecture を採用し、価格は Flash が $0.14/$0.28（入力/出力 100万トークン）と破格。 | [TechCrunch](https://techcrunch.com/2026/04/24/deepseek-previews-new-ai-model-that-closes-the-gap-with-frontier-models/) / [Simon Willison](https://simonwillison.net/2026/Apr/24/deepseek-v4/) |
| 3 | Cursor が $50B 評価で $2B 調達交渉 | a16z 共同リード、Nvidia・Thrive Capital・Battery Ventures が参加見通し。ARR は 2 月時点で $2B、年末には $6B+ を見込む。SpaceX からの $60B 買収提案も浮上。 | [CNBC](https://www.cnbc.com/2026/04/19/cursor-ai-2-billion-funding-round.html) / [TechCrunch](https://techcrunch.com/2026/04/22/how-spacex-preempted-a-2b-fundraise-with-a-60b-buyout-offer/) |
| 4 | Bitwarden CLI に Shai-Hulud 系のサプライチェーン攻撃 | `@bitwarden/cli@2026.4.0` が 4/22 の約 90 分間、悪性版として npm に流通。`bw1.js` が GitHub/npm トークン・SSH 鍵・.env・シークレットを窃取。CI/CD の GitHub Action 悪用が起点。利用者は秘密情報の即時ローテーションが必要。 | [The Hacker News](https://thehackernews.com/2026/04/bitwarden-cli-compromised-in-ongoing.html) / [Socket](https://socket.dev/blog/bitwarden-cli-compromised) |
| 5 | Vivaticket ランサムウェアでルーブル等 3,500 施設に影響 | RansomHouse が仏子会社 Irec SAS 経由で侵入。ルーブル・オルセー・エッフェル塔・ノートルダム等の予約系を停止させ、氏名・メール・予約履歴等を窃取。決済情報は流出未確認。 | [Cybernews](https://cybernews.com/cybercrime/ransomware-attack-on-vivaticket-disrupts-louvre-and-major-european-museums/) / [TechRadar](https://www.techradar.com/pro/security/top-museums-hit-by-apparent-cyberattack-on-vivaticket-louvre-and-other-institutions-affected) |
| 6 | LMDeploy の SSRF が実環境で活発に悪用 | CVE-2026-33626（CVSS 7.5）。LLM 推論サーバーで広く使われる LMDeploy がターゲットに。 | [The Hacker News](https://thehackernews.com/) |
| 7 | Iran が $30B Stargate AI データセンターへの攻撃を示唆 | OpenAI / Nvidia 等が出資する超大型 AI インフラ計画に対する物理脅威が顕在化、地政学リスクが AI インフラの新たなアタックサーフェスに。 | [Tech Startups](https://techstartups.com/2026/04/24/top-tech-news-today-april-24-2026/) |
| 8 | Nvidia 時価総額が再び $5T 大台、半導体 18 営業日続伸 | Intel の好決算（株価 +23%）が引き金に S&P500・Nasdaq が史上最高値。AI 関連の集中度が一段と上昇。 | [Yahoo Finance](https://finance.yahoo.com/markets/stocks/live/stock-market-today-friday-april-24-224547261.html) / [TheStreet](https://www.thestreet.com/latest-news/stock-market-today-apr-24-2026-updates) |
| 9 | AWS が Google Cloud と Multicloud 連携を簡素化 | ハイパースケーラー間の運用統合がついに進展。マルチクラウド前提の企業 IT に追い風。Q4'25 のクラウドインフラ投資は前年比 +29%。 | [Network World](https://www.networkworld.com/article/4098773/aws-finally-moves-to-simplify-multicloud-operations-with-google.html) |
| 10 | Linux Foundation の OSS エージェント Goose 1.2 が登場 | MCP サーバーの自動検出を実装し、ローカルファースト実行のセットアップ摩擦を大幅に低減。OSS エージェント開発のデファクト争いが本格化。 | [Fazm Blog](https://fazm.ai/blog/open-source-ai-projects-releases-updates-april-2026) |

## World News

| # | トピック | 概要 | ソース |
|---|---------|------|--------|
| 1 | 米イラン交渉、米代表団のパキスタン訪問が中止に | Trump がイラン側との直接会談中止を発表し、電話協議に切替。停戦は水曜に期限を迎える見通しで、ウラン濃縮の停止と備蓄引渡しを巡って対立継続。 | [CNN](https://www.cnn.com/2026/04/25/world/live-news/iran-war-israel-pakistan-talks) / [Al Jazeera](https://www.aljazeera.com/news/liveblog/2026/4/25/iran-war-live-tehrans-fm-in-islamabad-us-says-envoys-to-travel-for-talks) |
| 2 | War Powers Act の 60 日期限が 5/1 に到来 | 議会承認を経ていない対イラン軍事行動が法的タイムリミットを迎え、共和党内の結束にも変化の可能性。 | [CNN](https://www.cnn.com/2026/04/25/politics/war-powers-act-trump-iran-war-congress-analysis) |
| 3 | ロシア大規模空襲でウクライナに死者 7・負傷 57 名超 | ドニプロが最大被害（死者 8・負傷 49）。Tu-95MS による巡航ミサイル、計 619 機の無人機と 47 発のミサイル投入のうち 610 を迎撃。 | [Al Jazeera](https://www.aljazeera.com/news/2026/4/25/overnight-russian-attacks-on-ukraine-kill-five-wound-over-30) |
| 4 | EU が €90B（$106B）のウクライナ向け融資を承認 | ハンガリーの拒否権撤回を受け 2 年分の経済・軍事支援を確保。同時にロシア向けに 20 回目の制裁パッケージ（暗号資産分野含む）を採択。 | [NPR](https://www.npr.org/2026/04/24/nx-s1-5798455/eu-approves-a-106-billion-loan-package-to-help-ukraine-after-hungary-lifts-its-veto) / [Consilium](https://www.consilium.europa.eu/en/press/press-releases/2026/04/23/russia-s-war-of-aggression-against-ukraine-20th-round-of-stern-eu-sanctions-hits-energy-military-industrial-complex-trade-and-financial-services-including-crypto/) |
| 5 | ブルガリアで親露派 Radev 政党が地滑り的勝利 | 得票率 44.7%、議会 240 議席のうち約 130 を獲得見込み。EU/NATO 加盟国で対露関係再構築を掲げる政権が誕生し、ウクライナ支援に影響の可能性。 | [CNN](https://www.cnn.com/2026/04/20/europe/bulgaria-election-radev-wins-pro-russian-intl) / [Washington Post](https://www.washingtonpost.com/world/2026/04/20/bulgaria-russia-election-victory-radev/) |
| 6 | S&P500・Nasdaq が史上最高値、半導体は 18 営業日続伸 | Intel +23% の決算サプライズ、Nvidia 時価総額 $5T 復帰、半導体集中の市場構造がさらに強化。 | [Motley Fool](https://www.fool.com/coverage/stock-market-today/2026/04/24/stock-market-today-april-24-s-and-p-500-and-nasdaq-set-new-highs-on-tech-surge/) |
| 7 | 米 3 月 CPI が 3.3%、消費者信頼感は史上最低 47.6 | エネルギー価格高騰（ガソリン $4 超）で 2024 年 5 月以来の高水準。Fed は 3.5–3.75% で据え置き、利下げ余地は限定的との見方。 | [Yahoo Finance](https://finance.yahoo.com/economy/policy/articles/fed-quietly-altered-march-inflation-123300030.html) |
| 8 | 中国経済 Q1 +5%、PBOC が貸出基準金利を 11 か月連続据え置き | 1 年物 LPR 3.0%、5 年物 3.5%。中東情勢の影響を見極め追加緩和は見送り。2026 年成長目標 4.5–5%（90 年代以降で最低）。 | [CNBC](https://www.cnbc.com/2026/04/20/china-keeps-benchmark-lending-rates-unchanged-as-economic-growth-revs-up-amid-mounting-middle-east-risk-mount-.html) |
| 9 | WFP が 10 か国の急性食糧不安を警告 | ガザ・スーダンが特に深刻、2026 年見通しは「暗澹」。 | [News.az](https://news.az/news/april-26-2026-a-day-of-memory-politics-and-global-signals) |
| 10 | チェルノブイリ原発事故から 40 年（4/26） | ウクライナでの追悼と並行して、原子力安全と地政学リスクが再注目。 | [News.az](https://news.az/news/april-26-2026-a-day-of-memory-politics-and-global-signals) |

## Japan Tech News

| # | トピック | 概要 | ソース |
|---|---------|------|--------|
| 1 | LINEヤフーが AI エージェント「Agent i」を提供開始 | 4/20 から月間 1 億ユーザー規模の LINE / Yahoo! JAPAN 双方からワンタップで呼び出せる統一 AI エージェントを始動。お買い物・おでかけ・天気など 7 領域の専門エージェントを展開し、6 月には記憶機能・タスク実行機能を追加、夏には法人向け「Agent i Biz」も予定。 | [LINEヤフー](https://www.lycorp.co.jp/ja/news/release/020366/) / [日経](https://www.nikkei.com/article/DGXZRSP706133_Q6A420C2000000/) |
| 2 | SoftBank が Brain Technologies と「Natural AI Phone」を 4/24 発売 | アプリグリッドを廃した AI ネイティブ OS「Natural OS」搭載端末を 5,000 店舗で展開。価格 ¥93,600、6.7 インチ OLED + 5G + Android 15 ベース。SoftBank が国内 1 年独占販売権を持つ。 | [SoftBank News](https://www.softbank.jp/en/sbnews/entry/20260420_01) / [GlobeNewswire](https://www.globenewswire.com/news-release/2026/04/17/3276211/0/en/Brain-Technologies-and-SoftBank-Launch-Natural-AI-Phone-in-Japan.html) |
| 3 | SoftBank が国産 LLM「Sarashina」× Oracle Alloy で主権 AI クラウドを 6 月提供 | SB Intuitions の Sarashina を Oracle Alloy ベースの「Cloud PF Type A」上で稼働。データ主権を確保した生成 AI を企業・自治体向けに展開。東日本 DC は 4 月稼働、西日本は 10 月予定。 | [SoftBank](https://www.softbank.jp/corp/news/press/sbkk/2026/20260416_02/) / [Oracle](https://www.oracle.com/jp/news/announcement/softbank-expands-ai-services-in-japan-with-oracle-alloy-2026-04-16/) |
| 4 | Microsoft が日本に $10B 投資、AI 人材 100 万人を 2030 までに育成 | 2026–2029 に AI インフラ・サイバーセキュリティ・人材で過去最大規模の対日投資。Sakura Internet・SoftBank が GPU を供給、NTT Data・NEC・Fujitsu・Hitachi と人材教育で連携。 | [Microsoft](https://news.microsoft.com/source/asia/2026/04/03/microsoft-deepens-its-commitment-to-japan-with-10-billion-investment-in-ai-infrastructure-cybersecurity-workforce/) / [The Japan Times](https://www.japantimes.co.jp/business/2026/04/03/companies/microsoft-ai-japan-investment/) |
| 5 | Rapidus に追加 6,315 億円、累計 1.63 兆円超の国家投資へ | NEDO が FY2026 計画と予算を承認（4/11）、北海道千歳の 2nm パイロットラインを安定化させ 2027 年後半量産を目指す。Japan-US 連携の短 TAT 製造技術と 2nm 用チップレット実装も対象。 | [Rapidus](https://www.rapidus.inc/en/news_topics/information/nedo-approves-rapidus-fy2026-plan-and-budget-for-2nm-semiconductor-projects/) / [Bloomberg](https://www.bloomberg.com/news/articles/2026-04-11/japan-bets-16-billion-to-propel-startup-rapidus-into-ai-chips) |
| 6 | 「国家情報会議」設置法案が衆院通過（4/23）、今国会で成立公算 | 首相を議長とする情報会議＋事務局「国家情報局」を設置。重要情報活動の調査・審議や外国勢力の影響工作対応の基本方針を決定。スパイ防止法・対外情報庁の創設に向けた第一歩と高市政権が位置付け。 | [日経](https://www.nikkei.com/article/DGXZQOUA221B10S6A420C2000000/) / [NHK](https://news.web.nhk/newsweb/na/na-k10015106361000) |
| 7 | LY Corp、164 OpenStack クラスタを「Flava」へ統合 | LINE「Verda」（130k VM/11k host/4 cluster）と Yahoo! Japan「YNW」（27k server/160k VM/160+ cluster）をアップストリーム準拠の単一クラウドへ集約。社内パッチを最小化し、必要な変更は upstream に還元する方針。 | [The Register](https://www.theregister.com/2026/04/07/ly_corp_openstack_consolidation) |
| 8 | スタートアップ大型調達相次ぐ — CRISP 37億円・マイクロニティ 22億円・ミツモア 30億円 | サラダ専門店 CRISP がロッテベンチャーズ等から 37 億円、AI でソフトウェア事業承継を進めるマイクロニティが 22 億円、専門家マッチングのミツモアが 30 億円（4/20–24 週）を調達。AI/DX 系の成長期ラウンドが活発化。 | [PR TIMES](https://prtimes.jp/main/html/rd/p/000000111.000037550.html) / [STARTUP DB](https://lp.startup-db.com/media/articles/20260330-0403) / [日経](https://www.nikkei.com/article/DGXZQOUC23AJ70T20C26A4000000/) |
| 9 | AI・人工知能 EXPO【春】が東京ビッグサイトで開幕（4/15–17） | NexTech Week 2026 春の中核展。生成 AI Hub・AI エージェント World・AI インフラゾーン等を擁し、「実務を動かす AI エージェント」へのフェーズ移行が前面に。300 社以上が出展。 | [NexTech Week 公式](https://www.nextech-week.jp/hub/ja-jp.html) / [AIsmiley](https://aismiley.co.jp/event_detail/nextech-2026-spring-tokyo0415/) |
| 10 | Microsoft 4 月パッチで CVE-2026-32201 が 0day 悪用、IPA が緊急注意喚起 | 4/15 公表のセキュリティ更新で悪用が確認済みの脆弱性を含む。IPA は被害拡大の懸念から至急の適用を呼びかけ。並行して産業サイバーセキュリティ研究会も第 10 回を開催（4/3）。 | [IPA](https://www.ipa.go.jp/security/security-alert/2026/0415-ms.html) / [METI](https://www.meti.go.jp/press/2026/04/20260403003/20260403003.html) |

## Japan General News

| # | トピック | 概要 | ソース |
|---|---------|------|--------|
| 1 | 岩手・大槌町 山林火災が 1,176ha に拡大、平成以降 2 番目の被害 | 4/22 に小鎚地区・吉里吉里地区でほぼ同時発生。湿度 8.7% まで低下するフェーン現象が背景。避難指示は人口の 1/4 に当たる 2,588 人、住宅 5 棟以上が被害。1,000 人超の規模で消火活動が継続。 | [NHK](https://news.web.nhk/newsweb/na/na-k10015107961000) / [日経](https://www.nikkei.com/article/DGXZQOUD244NF0U6A420C2000000/) / [岩手日報](https://www.iwate-np.co.jp/article/2026/4/23/192453) |
| 2 | 日経平均が史上初の 6 万円台、4/24 終値 59,716 円 | 4/23 にザラ場で初の 6 万円台に到達、夜間先物では 6 万 140 円を記録。半導体・AI 関連の集中度が一段と上昇。野村は年末見通しを 6 万円に上方修正。 | [Diamond Zai](https://diamond.jp/zai/articles/-/1066448) / [日経](https://www.nikkei.com/markets/worldidx/chart/nk225/) |
| 3 | 日銀 4/27–28 会合は 0.75% 据え置き濃厚、利上げ判断は 6 月に持ち越し | 中東情勢の影響を見極めるため利上げを見送る公算。展望レポートは物価見通しが焦点。事前に「需給ギャップ」「中立金利」「コア指標」の論文 3 本を公表し利上げ気運を醸成。 | [日経](https://www.nikkei.com/article/DGXZQOUB2116H0R20C26A4000000/) / [三井住友DSAM](https://www.smd-am.co.jp/market/ichikawa/2026/04/irepo260422/) |
| 4 | ドル円 159 円台後半で高止まり、GW 介入警戒高まる | 4/24 終値 159.38 円。160 円手前で上値を抑えられつつ下値も底堅い。2024 年 GW の介入実績から市場は警戒を強めている。 | [外為どっとコム](https://www.gaitame.com/media/entry/2026/04/25/120000) / [みんかぶFX](https://fx.minkabu.jp/news/365435) |
| 5 | 高市政権 就任半年、衆院選圧勝後の高支持率を維持 | 2 月の衆院選で女性初の首相として圧勝。物価高対策を柱とする 2025 年度補正予算と 2026 年度予算（過去最大）を成立させた。木原官房長官は「強い経済・強い外交安保」の半年と総括。 | [時事通信](https://www.jiji.com/jc/article?k=2026042000906&g=pol) / [nippon.com](https://www.nippon.com/ja/in-depth/d01221/) |
| 6 | 高市首相、イランと首脳級会談を調整 — 中東情勢の沈静化目指す | 4/6 に「トップレベル会談を含めあらゆる方法を追求」と発言。茂木外相はクウェート外相との電話会談で連携を確認。日本は原油代替調達を進め、5 月には過半の代替調達に目処。 | [Bloomberg](https://www.bloomberg.com/jp/news/articles/2026-04-06/TD1QQHT9NJLU00) / [J-Defense](https://j-defense.ikaros.jp/docs/mod/005052.html) |
| 7 | 4 月月例経済報告 — 公共投資を「底堅い」から「堅調」に上方修正 | 「景気は緩やかに回復」の総括判断は据え置き。インフラ支出が景気を下支え。中東情勢の影響注視を強調し、原油高による企業収益圧迫リスクを警戒。 | [moneybits](https://moneybits.jp/2026/04/23/japan-economy-april-outlook-2026/) |
| 8 | 2025 年度輸出が過去最高 113 兆円、3 月の半導体は前年比 +51.7%（対中） | AI ギガサイクル下で半導体・電子部品輸出が約 +40%、特に対中で +51.7%。3 月総輸出は前年比 +11.7% で 7 か月連続増。一方で自動車は米 15% 関税の影響を受ける。 | [Reuters / Investing](https://www.investing.com/news/economy-news/japans-exports-expand-117-in-march-on-brisk-demand-higher-prices-4627974) / [The Japan Times](https://www.japantimes.co.jp/business/2026/02/18/economy/japan-exports-rise-china/) |
| 9 | 六本木女性殺害事件、8 年経て容疑者を逮捕 — マレーシアから帰国 | 警視庁は 4/25、2018 年に六本木のマンションで当時 29 歳の女性を殺害したとして当時の交際相手・高橋伸明容疑者（47）を殺人容疑で逮捕。マレーシア当局拘束を経て国際手配の身柄を移送。 | [朝日新聞](https://topics.smt.docomo.ne.jp/article/asahi/nation/ASV4S3FLHV4SUTIL015M) / [NHK](https://news.web.nhk/newsweb) |
| 10 | 4/26 の天気 — 西日本で雨強まる、北日本は気温上昇 | 本州南岸を通る低気圧の影響で九州〜近畿を中心に雨、局地的に強雨の見込み。関東は午前晴れ間あり、北日本は晴れて気温が上昇。 | [ウェザーニュース](https://weathernews.jp/news/202604/260011/) |

## Deep Dive

- [DeepSeek V4 — フロンティアモデルの 1/10 価格を実現した MoE と Hybrid Attention](./deepseek-v4-hybrid-attention.md)
- [Bitwarden CLI を襲った Shai-Hulud 系サプライチェーン攻撃の構造](./bitwarden-cli-shai-hulud-supply-chain.md)
- [大槌町 山林火災 — 平成以降 2 番目の被害に至った経緯と複合災害の構造](./jp-otsuchi-wildfire.md)
- [LINEヤフー Agent i — 月間 1 億ユーザー基盤に乗せた統一 AI エージェントの設計](./jp-line-yahoo-agent-i.md)
