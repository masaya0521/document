# VMware脆弱性とGridTideマルウェア — 高まるサイバーセキュリティリスク

- **日付**: 2026-03-06
- **カテゴリ**: Tech
- **ソース**: [The Hacker News](https://thehackernews.com/2026/02/google-disrupts-unc2814-gridtide.html), [Google Cloud Blog](https://cloud.google.com/blog/topics/threat-intelligence/disrupting-gridtide-global-espionage-campaign), [Cyber Security Review](https://www.cybersecurity-review.com/news-march-2026/)

## 概要

2026年3月初旬、サイバーセキュリティ分野で複数の深刻な脅威が明らかになった。Googleが中国関連のサイバースパイ活動「GridTide」を発見・阻止し、VMware Aria Operationsの高深刻度脆弱性が実際に悪用されていることが確認された。さらにイラン紛争に関連したハクティビスト活動も急増しており、サイバーセキュリティのリスクが複合的に高まっている。

## 詳細

### GridTideマルウェアによる大規模サイバースパイ活動

**攻撃者**: UNC2814（中国関連の脅威アクター、少なくとも2017年から活動）

**標的**: 42カ国53組織。主に通信事業者と政府機関

**GridTideマルウェアの特徴**:
- C言語で開発されたバックドア
- Google Sheets APIをC2（コマンド&コントロール）通信チャネルとして悪用
- スプレッドシートのセルにコマンドを書き込み、窃取データを読み取る手法でC2通信を偽装
- ファイルのアップロード/ダウンロード、任意のシェルコマンド実行をサポート
- 個人識別情報（PII）を含むエンドポイントに展開され、要注意人物の監視に利用

**Googleの対応**:
- 攻撃者が制御する全てのCloud Projectを終了
- パートナーと協力し、UNC2814の既知インフラを無効化（ドメインのシンクホール化を含む）
- 攻撃者アカウントを無効化し、C2用Google Sheetsへのアクセスを取り消し

### VMware Aria Operationsの脆弱性（CVE-2026-22719）

- **深刻度**: CVSS 8.1（高）
- **種類**: コマンドインジェクション
- **影響**: 未認証の攻撃者が任意のコマンドを実行可能
- **状況**: CISAが既知の悪用脆弱性（KEV）カタログに追加、実際の攻撃での悪用を確認

### Laravel偽装パッケージによるRAT配布

- PackagistのPHPパッケージがLaravelユーティリティに偽装
- Windows、macOS、Linuxの全OSで動作するリモートアクセストロイの木馬（RAT）を配布
- オープンソースサプライチェーン攻撃の新たな事例

### イラン紛争関連のハクティビスト活動急増

- Keymous+とDieNetの2グループが全攻撃活動の約70%を占める
- 2月28日〜3月2日の間に報復的なハクティビスト活動が急増
- CISAは政府シャットダウンや人員削減の影響で対応能力が低下

## 今後の注目点

- GridTide以外のUNC2814の攻撃インフラが残存している可能性（2017年から活動）
- Google Sheets等の正規サービスをC2に悪用する手法の拡散リスク
- VMware Aria Operations脆弱性の未パッチ環境への攻撃継続
- イラン紛争の長期化に伴うサイバー攻撃のさらなるエスカレーション
- CISAの人員・予算削減がサイバー防衛に与える影響
- オープンソースパッケージレジストリの信頼性確保の課題
