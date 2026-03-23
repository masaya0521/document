# AI セキュリティの新たな脅威 — Trivy サプライチェーン攻撃

- **日付**: 2026-03-24
- **カテゴリ**: Tech
- **ソース**: [Aqua Security](https://www.aquasec.com/blog/trivy-supply-chain-attack-what-you-need-to-know/), [The Hacker News](https://thehackernews.com/2026/03/trivy-security-scanner-github-actions.html), [Wiz](https://www.wiz.io/blog/trivy-compromised-teampcp-supply-chain-attack), [CrowdStrike](https://www.crowdstrike.com/en-us/blog/from-scanner-to-stealer-inside-the-trivy-action-supply-chain-compromise/)

## 概要

2026年3月、広く利用されているオープンソース脆弱性スキャナー Aqua Security Trivy が大規模なサプライチェーン攻撃を受けた。「TeamPCP」と名乗る攻撃者が GitHub Actions の設定不備を起点に、Trivy のリリース自動化プロセスに侵入。悪意あるバージョンを配布し、CI/CD パイプラインから認証情報を窃取した。さらに攻撃は拡大し、44のリポジトリの改ざん、npm パッケージへのワーム配布にまで及んでいる。

## 詳細

### 攻撃のタイムライン

**2月下旬**: 攻撃者が Trivy の GitHub Actions 環境の設定不備を悪用し、特権アクセストークンを抽出。リリース自動化プロセスへの足がかりを確立。

**3月1日**: Trivy チームが先行するインシデントを公開し、認証情報のローテーションを実施。しかし、ローテーションが不完全であり、一部の有効な認証情報が攻撃者の手元に残った。

**3月19日 (~17:43 UTC)**: 攻撃者が本格的に行動を開始。
- `aquasecurity/trivy-action` の77タグ中76タグを強制プッシュで改ざん
- `aquasecurity/setup-trivy` の全7タグを改ざん
- 侵害された `aqua-bot` サービスアカウント経由で、悪意あるバイナリ v0.69.4 のリリースをトリガー

**3月22日**: Aqua Security の内部 GitHub 組織（aquasec-com）の全44リポジトリが一斉に改名・改ざん。

### マルウェアの挙動

悪意あるバージョンには「TeamPCP Cloud stealer」と自称するツールが含まれ、以下の動作を実行する:

1. **プロセスメモリダンプ**: Runner.Worker プロセスのメモリを読み取り
2. **認証情報収集**: SSH 鍵、クラウド認証情報、Kubernetes シークレットを収集
3. **暗号化**: AES-256 + RSA-4096 で収集データを暗号化
4. **外部送信**: リモートサーバーへデータを送出

### 二次被害の拡大

窃取されたデータを利用して、攻撃者は以下の二次攻撃を展開:
- 数十の npm パッケージを侵害
- 「CanisterWorm」と呼ばれる自己増殖型ワームを配布
- Docker イメージ経由でのインフォスティーラーの拡散
- Kubernetes 環境でのワイパー（データ破壊）攻撃

### 教訓と対策

この事件は、セキュリティツール自体がサプライチェーン攻撃の標的になるという深刻なリスクを浮き彫りにした。

- **GitHub Actions のタグ固定**: バージョンタグではなくコミットハッシュで Actions を参照する
- **認証情報ローテーションの徹底**: 部分的なローテーションでは残存リスクが解消されない
- **CI/CD パイプラインのシークレット管理**: ランナー環境にシークレットを平文で残さない
- **サプライチェーンの多層防御**: スキャナーの出力だけでなく、スキャナー自体の完全性も検証する

## 今後の注目点

- Aqua Security の完全なインシデントレポートと再発防止策の公表
- CanisterWorm の感染範囲の全容解明 — npm エコシステムへの影響はまだ調査中
- GitHub Actions のセキュリティモデルに対するコミュニティの議論の行方
- 他のセキュリティスキャナー（Snyk, Grype 等）のサプライチェーンセキュリティ強化の動き
- SLSA や Sigstore 等のソフトウェアサプライチェーンセキュリティフレームワークの採用加速
