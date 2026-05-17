# Daily Digest — 2026-05-18

## Tech News

| # | トピック | 概要 | ソース |
|---|---------|------|--------|
| 1 | NGINX rewrite モジュールに 18 年潜伏した RCE 脆弱性 | `ngx_http_rewrite_module` のヒープバッファオーバーフロー（CVE-2026-42945, CVSS 9.2）が公表。`rewrite` 後の PCRE キャプチャと `?` を含む置換文字列の組み合わせで未認証 RCE が可能。NGINX Plus R32 P6 / OSS 1.30.1 で修正。 | [The Hacker News](https://thehackernews.com/2026/05/18-year-old-nginx-rewrite-module-flaw.html) |
| 2 | Google と SpaceX、軌道データセンター打ち上げで協議 | Google の Project Suncatcher（TPU 搭載衛星 81 基構想）に向け、SpaceX が打ち上げ提供で協議中と WSJ が報道。SpaceX は 2026 年後半に 1.75 兆ドル規模 IPO を準備、軌道コンピュートを投資家へ訴求。 | [TechCrunch](https://techcrunch.com/2026/05/12/report-google-and-spacex-in-talks-to-put-data-centers-into-orbit/) |
| 3 | Pwn2Own Berlin 2026、47 個の 0-day で 129.8 万ドルを支払い | DEVCORE が Microsoft Exchange のチェーン RCE などで 50.5 ポイントを獲得し Master of Pwn を制覇。Windows 11・Edge・LiteLLM など AI 製品も陥落。応募超過で 150 名以上が辞退する盛況。 | [Security Affairs](https://securityaffairs.com/192209/security/pwn2own-berlin-2026-day-two-385750-more-microsoft-exchange-falls-and-the-running-total-crosses-900k.html) |
| 4 | OpenAI、ChatGPT 内にセルフサーブ広告プラットフォームを提供開始 | 月間 9 億 WAU・有料 5,000 万人に対する直接マネタイズ手段が登場。同社は月次収益 20 億ドル規模に到達しており、IPO を見据えた収益多角化として注目。 | [AI Tools Recap](https://aitoolsrecap.com/Blog/MayNews2026.aspx) |
| 5 | GitHub Copilot、6/1 から AI Credits ベース課金へ移行 | エージェント実行・プレミアムモデル呼び出し・バックグラウンドタスクが従量制クレジットを消費する形へ。Copilot 有料契約は 470 万・前年比 +75%、Microsoft 内で GitHub 本体を超える事業に成長。 | [SD Times](https://sdtimes.com/) |
| 6 | AWS Kiro、Parallel Task Execution など 3 機能を追加 | spec-driven 開発を志向する Kiro が、独立タスクの並列実行・Quick Plan による要件/設計/タスク一括生成・ニューロシンボリック AI による Requirements Analysis を導入。 | [AWS News Blog](https://aws.amazon.com/blogs/aws/aws-weekly-roundup-whats-next-with-aws-2026-amazon-quick-openai-partnership-and-more-may-4-2026/) |
| 7 | Anthropic と Akamai が 18 億ドルのコンピュート契約 | 推論需要の急増に対応するため、Akamai のエッジ／クラウド計算資源を活用。AI ベンダーとエッジ事業者の長期契約として象徴的。 | [Bloomberg](https://www.bloomberg.com/news/articles/2026-05-08/anthropic-inks-1-8-billion-computing-deal-with-akamai) |
| 8 | 主要ハイパースケーラー 4 社、2026 年の AI capex を計 7,250 億ドル超に拡大 | Meta・Amazon・Microsoft・Alphabet の合算で前年比 +75% 超。データセンター・カスタムチップ・GPU・AI モデルへの傾斜投資が継続。 | [Tech Startups](https://techstartups.com/2026/05/15/top-tech-news-today-may-15-2026/) |
| 9 | npm `node-ipc` に難読化バックドアを含む悪意ある 3 バージョンが配布 | `9.1.6` / `9.2.3` / `12.0.1` で stealer/backdoor 挙動を確認。OSS サプライチェーンへの継続的脅威としてアラート。 | [The Hacker News](https://thehackernews.com/) |
| 10 | Cisco Catalyst SD-WAN Controller の認証バイパス、CISA KEV に追加 | CVE-2026-20182（認証バイパス）が悪用観測。FCEB 連邦機関は 5/17 までの修正が義務化された。 | [SecurityWeek](https://www.securityweek.com/) |

## World News

| # | トピック | 概要 | ソース |
|---|---------|------|--------|
| 1 | トランプ氏・習氏、北京での米中首脳会談を終了 | 「多くの問題を解決した」と発表する一方、台湾とイランで隔たりが残存。習氏は台湾を「最重要課題」と位置付け、扱いを誤れば「衝突」に至ると警告。 | [Euronews](https://www.euronews.com/2026/05/15/china-offers-us-to-help-open-strait-of-hormuz-but-warns-trump-over-taiwan) |
| 2 | ロシアのキーウ集合住宅へのミサイル攻撃で少なくとも 24 人死亡 | 開戦以来最悪規模のキーウ攻撃の一つ。停戦交渉の停滞が浮き彫りに。 | [Democracy Now!](https://www.democracynow.org/2026/5/15/headlines) |
| 3 | フィリピン上院、サラ・ドゥテルテ副大統領の弾劾裁判を 5/18 開廷 | 国内最有力政治一族が真っ向対立。地域政治の不安定化要因として国際的にも注目。 | [ABC News](https://abcnews.com/international) |
| 4 | イエメン暫定政府とフーシ派、1,600 人超の捕虜交換に合意 | 11 年に及ぶ内戦で最大規模の交換。中東情勢の数少ない緩和材料。 | [ABC News](https://abcnews.com/international) |
| 5 | イスラエル、ハマス軍事部門指導者の殺害を発表 | 2023 年 10/7 攻撃の「設計者の一人」と位置付け。ガザ情勢への影響が焦点。 | [Democracy Now!](https://www.democracynow.org/2026/5/15/headlines) |
| 6 | ラトビアのシリーニャ首相が辞任 | ウクライナのドローン墜落事案を契機とする政治危機を受けた辞任。NATO 東部の安定が論点に。 | [Wikipedia: 2026 in politics](https://en.wikipedia.org/wiki/2026_in_politics) |
| 7 | 米下院のイラン戦争権限決議、212-212 の同数で否決 | トランプ政権のイラン攻撃を制限する民主党側の試みは 3 度連続で失敗。 | [Democracy Now!](https://www.democracynow.org/2026/5/15/headlines) |
| 8 | BRICS 連続閣僚会合、イラン戦争を巡る意見対立で共同声明見送り | 多国間枠組みの結束力低下が顕在化。 | [Geopolitical Monitor](https://www.geopoliticalmonitor.com/) |
| 9 | 米 4 月 CPI が前年比 +3.8%、2023 年 5 月以来の高水準 | Fed の利上げ確率が市場で上昇（残り 2026 年で約 10bp の利上げを織り込み）。10 年債利回り急騰で S&P 500 は -1.24%。 | [Crestwood Advisors](https://www.crestwoodadvisors.com/may-2026-economic-and-market-update/) |
| 10 | 米 4 月雇用統計、115,000 人増・失業率 4.3% | 予想（55,000 人）を大きく上回るも、労働参加率は 2021 年 9 月以来の低水準に低下。雇用の質を巡る議論が継続。 | [TheStreet](https://www.thestreet.com/latest-news/stock-market-today-may-15-2026-updates) |

## Japan Tech News

| # | トピック | 概要 | ソース |
|---|---------|------|--------|
| 1 | ソフトバンク・NEC・ホンダ・ソニーが「日本AI基盤モデル開発」を設立 | 中核 4 社に加え三井住友・三菱 UFJ・みずほの 3 メガバンクと日本製鉄・神戸製鋼が出資。約 100 人の AI 技術者を集約し 1 兆パラメーター級のフィジカル AI 基盤モデルを目指す。政府は 2026 年度からの 5 年で約 1 兆円規模の支援枠を設定。 | [日本経済新聞](https://www.nikkei.com/article/DGXZQOUC1207B0S6A410C2000000/) |
| 2 | NTT、AI ネイティブ基盤「AIOWN」発表 | 現状約 300MW の IT 電力容量を 2033 年度に約 1GW へ 3 倍超拡大する計画。生成 AI 推論需要を見越したインフラ投資としては国内最大級。 | [ケータイ Watch](https://k-tai.watch.impress.co.jp/docs/news/2104930.html) |
| 3 | デジタル庁、ガバメント AI「源内」を開発 | 行政職員が業務で生成 AI を安全に活用するための内製アプリ連携基盤。経産省・総務省 AI ガイドラインを前提に「導入」から「安全運用」フェーズへ移行。 | [DESIGN STUDIO garden](https://note.com/dsg_id/n/n17e11f5c7093) |
| 4 | 第 4 回日 EU デジタルパートナーシップ閣僚級会合の結果公表 | 5/7 開催分の結果をデジタル庁が公表。JP PINT のグローバル取組・民間事業者取組も更新。 | [デジタル庁](https://www.digital.go.jp/news) |
| 5 | NTT データ経営研究所、金融機関向け AI 導入コンサル全 18 サービス開始 | メガバンク・地銀・証券会社を対象に 2026/5/7 から提供開始。生成 AI ガバナンスから業務適用までを包括。 | [NTTデータ経営研究所](https://www.nttdata-strategy.com/newsrelease/260507/) |
| 6 | 読売新聞・帝国データバンク共同調査、国内企業の 3 割が生成 AI を業務利用 | 文章作成・情報収集が中心。導入企業は業務効率化とコスト削減を実感。「導入する/しない」から「どう運用するか」へフェーズシフト。 | [DESIGN STUDIO garden](https://note.com/dsg_id/n/n17e11f5c7093) |
| 7 | 動画生成 AI「Runway」が東京進出、日本アニメの知財活用を支援 | 国内アニメ IP を学習・生成パイプラインへ取り込む狙い。日本のクリエイティブ業界における AI 活用と権利処理の議論を加速。 | [DESIGN STUDIO garden](https://note.com/dsg_id/n/n17e11f5c7093) |
| 8 | 建設テック Kizuki、日本初の 3D プリント 2 階建て住宅「Stealth House」を公開 | 50㎡を 14 日で印刷。20 社超と連携し耐震基準もクリア。建設業の人手不足対策として注目。 | [CNN Business](https://www.cnn.com/2026/05/07/business/japans-3d-printing-construction-sector-crisis-hnk-spc) |
| 9 | メルカリ、26 年 6 月期 3Q 累計で最終利益 194 億円 (+65.6%) | 1-3 月期は最終利益 88.4 億円で前年比 2 倍。米国事業と国内マーケットプレイスの双方が寄与。 | [Yahoo!ファイナンス](https://finance.yahoo.co.jp/news/detail/f5415e108f5f2f0e94811ddf02f81927c15bbb46) |
| 10 | LINE ヤフー、業種特化型「LINE Restaurant Plus」「LINE Beauty Plus」を 6 月開始 | 飲食・美容業界向けに予約・顧客管理・販促を一気通貫で提供するパッケージサービス。 | [LY Corporation](https://www.lycorp.co.jp/ja/news/release/2026/) |

## Japan General News

| # | トピック | 概要 | ソース |
|---|---------|------|--------|
| 1 | G7 財務相・中銀総裁会議、仏パリで 5/18 開幕 | 片山さつき財務相と植田日銀総裁が出席。AI を悪用した金融サイバー攻撃対策・中東危機を踏まえた原油安定・重要鉱物供給網（脱中国）が主要議題。 | [日本経済新聞](https://www.nikkei.com/article/DGXZQOUA149QQ0U6A510C2000000/) |
| 2 | 党首討論を 5/20 開催と正式決定、最多 6 野党党首が高市首相と論戦 | 国民・玉木代表 12 分、中道改革連合・小川代表 10 分、立憲・水岡代表 9 分など。衆院選後初の党首討論で「政権能力」が焦点。 | [日本経済新聞](https://www.nikkei.com/article/DGXZQOUA156M60V10C26A5000000/) |
| 3 | 政府・日銀の為替介入、4/30 以降合計 8.65 兆〜10.08 兆円規模と推計 | 政府は 1 ドル 160 円を防衛ラインに設定。GW 連休中の 5/4・5/6 にも円買い介入の動き。 | [Bloomberg](https://www.bloomberg.com/jp/news/articles/2026-05-08/TEOZJZT9NJLS00) |
| 4 | 日銀、4 月会合で政策金利を据え置き 物価上振れ懸念は強まる | 「主な意見」では原油高騰に伴う早期利上げを求める声が目立つ。次回会合は 6/15・16。 | [日本経済新聞](https://www.nikkei.com/article/DGXZQOUB121XI0S6A510C2000000/) |
| 5 | ヘリカルフュージョン、核融合発電開発で約 27 億円を調達 | 鴻池運輸・三谷産業などを引受先とする第三者割当増資。日本発の核融合スタートアップとして注目。 | [日本経済新聞](https://www.nikkei.com/article/DGXZQOUC309630Q6A430C2000000/) |
| 6 | Qubitcore（量子コンピューター）、SBI インベストメント等から 15.3 億円調達 | 横浜拠点の量子計算スタートアップ。国産量子ハードウェア開発を加速。 | [日本経済新聞](https://www.nikkei.com/article/DGXZQOUC309630Q6A430C2000000/) |
| 7 | ヘンリー（クラウド型電子カルテ）、30 億円を調達 | Angel Bridge・グロービス等が引受。中小病院 DX 市場での競争激化。 | [日本経済新聞](https://www.nikkei.com/article/DGXZQOUC14BB40U6A510C2000000/) |
| 8 | 広島・福山の山林火災、5/18 朝時点で鎮火見通し立たず | 消火活動継続中。乾燥した気象条件と地形が消火を難しくしている。 | [時事ドットコム](https://www.jiji.com/jc/archives?g=soc_archive_0) |
| 9 | Microsoft 5 月月例で 118 件の脆弱性に対応、IPA も注意喚起 | 権限昇格 57 件・RCE 29 件を含む。Exchange Server には悪用観測の脆弱性も。 | [Security NEXT](https://www.security-next.com/184334) |
| 10 | 国内情報漏えいが相次ぐ 5 月上旬 | 新潟市の個人情報漏えい、東北大学のサーバー不正アクセス、2 りんかん・メットライフ生命の漏えい等が連続発覚。 | [Security NEXT](https://www.security-next.com/) |

## Deep Dive

- [NGINX rewrite モジュールの 18 年潜伏脆弱性 (CVE-2026-42945)](./nginx-rewrite-rce-cve-2026-42945.md)
- [Google + SpaceX 軌道データセンター構想 (Project Suncatcher)](./google-spacex-orbital-data-centers.md)
- [日本連合「日本AI基盤モデル開発」──米中対抗の国産フィジカル AI 構想](./jp-japan-ai-foundation-model.md)
- [円安と利上げ見送りの綱引き──2026 年 GW の 10 兆円規模為替介入](./jp-fx-intervention-and-boj-policy.md)
