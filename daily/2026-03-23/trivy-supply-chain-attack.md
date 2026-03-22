# Trivy サプライチェーン攻撃: OSS セキュリティの新たな脅威

- **日付**: 2026-03-23
- **カテゴリ**: Tech
- **ソース**: [Wiz Blog](https://www.wiz.io/blog/trivy-compromised-teampcp-supply-chain-attack), [The Hacker News](https://thehackernews.com/2026/03/trivy-security-scanner-github-actions.html), [StepSecurity](https://www.stepsecurity.io/blog/trivy-compromised-a-second-time---malicious-v0-69-4-release)

## 概要

2026年3月19日、広く利用されているコンテナ脆弱性スキャナ「Trivy」（Aqua Security）が「TeamPCP」と名乗る脅威アクターにより侵害された。攻撃者は Trivy 本体の v0.69.4 リリースと GitHub Actions の75のタグを書き換え、認証情報窃取マルウェアを注入した。さらに窃取した npm 公開トークンを使って「CanisterWorm」と呼ばれるワームを47の npm パッケージに拡散させるなど、被害が連鎖的に拡大した。

## 詳細

### 攻撃の手法

攻撃は高度なサプライチェーン攻撃として実行された。

1. **初期侵入**: 自律 AI ボット「hackerbot-claw」が、Trivy の GitHub Actions ワークフローに存在する `pull_request_target` の設定ミスを悪用し、Personal Access Token (PAT) を窃取
2. **リポジトリ乗っ取り**: 窃取した PAT を使用してリポジトリへの完全なアクセスを取得
3. **なりすましコミット**: 正規の開発者（rauchg、DmitriyLewen）になりすました偽のコミットを actions/checkout および aquasecurity/trivy にプッシュ
4. **タグ書き換え**: aquasecurity/trivy-action リポジトリの76タグ中75タグを悪意あるバージョンに強制プッシュ
5. **悪意あるリリース**: Trivy 本体の v0.69.4 に認証情報窃取マルウェアを注入

### マルウェアの機能

注入されたマルウェア「TeamPCP Cloud stealer」は以下の動作を行う。

- **Runner.Worker プロセスメモリのダンプ**: CI/CD 実行環境のプロセスメモリを読み取り
- **認証情報の収集**: SSH キー、クラウド認証情報（AWS、GCP、Azure）、Kubernetes シークレットを収集
- **データの暗号化と窃取**: AES-256 + RSA-4096 で暗号化し、外部サーバーに送信

### 2度目の侵害

特に深刻なのは、これが Trivy にとって2度目の侵害であったことだ。Aqua Security は最初の侵害発見後にシークレットとトークンのローテーションを実施したが、ローテーションがアトミック（一括完了）ではなかったため、その隙間を突いて2度目の攻撃が成功した。

### 連鎖的被害: CanisterWorm

攻撃は GitHub Actions に留まらず、npm エコシステムにも波及した。窃取した npm 公開トークンを使用して「CanisterWorm」と呼ばれるセルフスプレッディングワームが47の npm パッケージに注入された。これにより、Trivy を直接利用していない開発者にも被害が拡大する構造となった。

### 影響範囲

Trivy は世界中の CI/CD パイプラインで広く利用されている脆弱性スキャナであり、影響を受けた可能性のあるプロジェクトは膨大な数に上る。Wiz Research は3月22日時点でも TeamPCP の活動を引き続き追跡中と報告している。

## 今後の注目点

- **被害規模の全容解明**: 窃取された認証情報を使った二次被害の範囲
- **`pull_request_target` の設定ミスへの業界対応**: 同様の設定ミスを持つ他の OSS プロジェクトの洗い出しと修正
- **AI ボットによる攻撃の進化**: hackerbot-claw のような自律 AI ツールが脆弱性発見・悪用を自動化するトレンドの加速
- **GitHub Actions のセキュリティ強化**: タグの不変性やタグ署名など、プラットフォームレベルでの対策
- **シークレットローテーションのベストプラクティス**: アトミックなローテーション手順の確立と自動化
- **npm エコシステムへの波及**: CanisterWorm の完全な封じ込めと影響を受けたパッケージの特定
