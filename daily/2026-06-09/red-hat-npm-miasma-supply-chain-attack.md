# Red Hat npm サプライチェーン攻撃「Miasma」— 自己増殖する認証情報窃取ワーム

- **日付**: 2026-06-09
- **カテゴリ**: Tech
- **ソース**: [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/2026/06/02/preinstall-persistence-inside-red-hat-npm-miasma-credential-stealing-campaign/) / [The Hacker News](https://thehackernews.com/2026/06/miasma-supply-chain-compromises.html) / [Orca Security](https://orca.security/resources/blog/red-hat-npm-supply-chain-attack/)

## 概要

2026年6月1日、Red Hat 従業員の GitHub アカウントが乗っ取られたことを起点に、`@redhat-cloud-services` スコープの公式 npm パッケージ32個（96バージョン）へ認証情報窃取ワームが注入された。攻撃は「Miasma: The Spreading Blight」と名付けられ、`preinstall` ライフサイクルフックで自動実行される点と、盗んだトークンで別パッケージ・リポジトリへ自己増殖する点が特徴。汚染パッケージの累計ダウンロードは週あたり約11.7万回に達していた。

## 詳細

### 侵入経路

攻撃者は Red Hat 従業員の GitHub アカウントを奪取し、RedHatInsights の3リポジトリ（`frontend-components`、`javascript-clients`、`platform-frontend-ai-toolkit`）に悪意ある GitHub Actions ワークフローを仕込んだ。これを足がかりに npm パッケージへペイロードを混入させた。

### マルウェアの動作

- `preinstall` フックで起動するため、**アプリケーションコードが実行される前**に 4.2MB の難読化 JavaScript ペイロードが走る。
- 包括的な認証情報スイープを実行。標的は以下を含む:
  - GitHub Actions トークン
  - AWS アクセスキー / セッショントークン
  - GCP アプリケーションデフォルト認証情報 / サービスアカウントキー
  - Azure サービスプリンシパル / マネージド ID トークン
  - HashiCorp Vault トークン
  - Kubernetes サービスアカウント / kubeconfig
  - npm / PyPI 公開トークン、SSH 秘密鍵、Docker レジストリ認証情報、GPG 鍵、全 `.env` ファイル

### 自己増殖（ワーム性）

CI/CD 環境では GitHub Actions ランナーのメモリからシークレットを掻き集め、パスワードレス sudo で権限昇格し、偽造した SLSA(Supply-chain Levels for Software Artifacts) provenance を付けて汚染パッケージを再公開。盗んだトークンでさらに別のパッケージ・リポジトリを侵害し、カスケード的にサプライチェーンへ波及した。

### 文脈

2026年版 State of Open Source Report によれば、OSS 脆弱性はコードベースあたり581件へほぼ倍増し、監査対象の87%が何らかのセキュリティリスクを抱える。Miasma はこうした OSS サプライチェーンの脆弱性が現実の大規模インシデントに転化した典型例といえる。

## 今後の注目点

- 盗まれたクラウド/CI 認証情報を悪用した二次被害（横展開）の有無
- `preinstall` フックを悪用するインストール時実行マルウェアへの防御策（`--ignore-scripts` の徹底、隔離ビルド環境）
- SLSA provenance の偽造耐性 — provenance だけでは信頼の根拠にならない問題
- npm レジストリ側の公開トークン保護・2FA 強制・異常公開検知の強化
- 自社の依存関係に `@redhat-cloud-services` 系パッケージが含まれていないかの緊急監査
