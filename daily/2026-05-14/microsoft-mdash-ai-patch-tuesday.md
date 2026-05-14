# Microsoft MDASH: AI エージェントが脆弱性を見つける時代の Patch Tuesday

- **日付**: 2026-05-14
- **カテゴリ**: Tech
- **ソース**: [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/2026/05/12/defense-at-ai-speed-microsofts-new-multi-model-agentic-security-system-finds-16-new-vulnerabilities/) / [The Hacker News](https://thehackernews.com/2026/05/microsofts-mdash-ai-system-finds-16.html) / [Help Net Security](https://www.helpnetsecurity.com/2026/05/13/microsoft-mdash-agentic-ai-security-system/)

## 概要

2026 年 5 月の Patch Tuesday（5/13）で Microsoft は 120 件の脆弱性を一括修正した。注目すべきは件数ではなく「**誰が**それを見つけたか」だ。Windows ネットワーク・認証層に存在した 16 件の脆弱性（うち Critical RCE が 4 件）は、Microsoft 社内の自律型 AI エージェントシステム **MDASH（multi-model agentic scanning harness）** によって発見された。MSRC 過去 5 年の確認済み脆弱性に対し、`clfs.sys` で 96%、`tcpip.sys` で 100% のリコール率を達成し、業界ベンチマーク CyberGym では 88.45% でトップを獲得。AI エージェントが「脆弱性を見つける側」に立つことを明確に示した事例である。

## 詳細

### MDASH のアーキテクチャ

MDASH は **model-agnostic（モデル非依存）** に設計された 3 段階のパイプラインで動作する。

1. **Prepare ステージ**: ソースを取り込み、攻撃面（attack surface）と脅威モデル（threat model）を抽出。スキャン対象の境界を AI 自身が定義する。
2. **Scan ステージ**: 脆弱性クラスごとに専門化された "auditor agent"（例: メモリ安全担当・認証担当・パーサ担当）を候補コードパス上で並列実行。
3. **Prove ステージ**: 発見された候補に対して動的に pre-condition を検証し、実際にトリガーする入力を構成して exploitable であることを証明する。

ポイントは「報告で終わらせない」設計だ。**Prove ステージで再現可能な PoC まで自動生成する**ことで、人間のセキュリティエンジニアの確認負荷を最小化している。Microsoft はこれを "Defense at AI speed"（AI スピードでの防衛）と表現している。

### 今回発見された 16 件の脆弱性

- 内訳: **kernel-mode 10 件 / user-mode 6 件**
- 範囲: Windows TCP/IP スタック、IKEEXT IPsec サービス、HTTP.sys、Netlogon、DNS resolution、Telnet client
- 多くが「**認証なしのネットワーク到達**」が可能な構成。例:
  - **CVE-2026-41096**: Windows DNS heap-based buffer overflow（CVSS 9.8）
  - **CVE-2026-41089**: Windows Netlogon stack-based buffer overflow — domain controller に細工リクエストを送るだけで RCE
- これらは 5 月 Patch Tuesday の 120 件のうちの中核であり、Critical 17 件の品質を一段引き上げている。

### なぜ「AI が脆弱性を見つける」が重要なのか

セキュリティ業界ではこれまで、AI を「攻撃側が悪用するリスク」として論じる文脈が多かった。実際 5/11 には Google Threat Intelligence Group が AI を用いた mass exploitation 試行の阻止を発表したばかりだ。今回の MDASH は反対側、すなわち「**防衛側のスケール**」を示した。

従来のファジング・シンボリック実行・静的解析と異なり、MDASH の auditor agent は「脆弱性クラスごとの仮説」を持ったエージェントとして動く。これは Anthropic 系・OpenAI 系の他の "agentic security" 取り組み（Anthropic Mythos など）との競争領域でもある。Neowin は MDASH が Anthropic Mythos を超えると報じている。

### 開発者・運用者への影響

- **Patch Tuesday の規模が今後さらに膨れる**: AI による発見ペースの加速で、月次パッチの件数とインパクトが拡大することが Microsoft 自身からアナウンスされている。CI / イメージ更新のオペレーションが追従できる体制づくりが必要。
- **DC / DNS / IPsec を露出するサーバの即時パッチ適用**: 認証なしネットワーク RCE が複数含まれており、攻撃側のリバースエンジニアリングが進めば exploit 化が早い。
- **「AI スキャン耐性」が設計品質指標になりつつある**: 内部品質ゲートに AI agentic scan を組み込む流れが大手から始まる可能性が高い。

## 今後の注目点

- Microsoft が MDASH を社外（顧客・OSS コミュニティ）に開放する範囲と価格設定
- Anthropic Mythos / Google の対抗システムとのベンチマーク競争
- EU が GPT-5.5-Cyber の評価アクセスを受けた一方、Anthropic Mythos が保留中の構図は、防御 AI へのガバナンスがどう敷かれるかの観測ポイント
- AI 発見系 CVE の「**開示タイミング**」と「**ベンダー間調整**」のあり方（fuzzing と異なり、エージェント自身が説明可能な脅威モデルを出すため、責任ある開示プロセスが変容する可能性）
- 攻撃側が同等の agentic scanning を稼働させた場合の **N-day から 0-day までの圧縮**
