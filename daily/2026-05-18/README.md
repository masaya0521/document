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

## Deep Dive

- [NGINX rewrite モジュールの 18 年潜伏脆弱性 (CVE-2026-42945)](./nginx-rewrite-rce-cve-2026-42945.md)
- [Google + SpaceX 軌道データセンター構想 (Project Suncatcher)](./google-spacex-orbital-data-centers.md)
