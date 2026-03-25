# LiteLLM サプライチェーン攻撃 — TeamPCP の連鎖的侵害の全容

- **日付**: 2026-03-26
- **カテゴリ**: Tech
- **ソース**: [The Hacker News](https://thehackernews.com/2026/03/teampcp-backdoors-litellm-versions.html)

## 概要

2026年3月24日、脅威アクター TeamPCP が Python パッケージ litellm の PyPI アカウントを侵害し、バックドア入りのバージョン（v1.82.7 / v1.82.8）を公開した。この攻撃は Aqua Security の Trivy スキャナや Checkmarx の GitHub Actions を経由した多段階のサプライチェーン攻撃の一環であり、月間9500万ダウンロード、クラウド環境の36%に影響を及ぼす規模となった。

## 詳細

### 攻撃の連鎖

TeamPCP の攻撃は単発ではなく、数週間にわたる連鎖的なサプライチェーン攻撃だった。

1. **Trivy の侵害**: Aqua Security のコンテナスキャナ Trivy の GitHub Action を侵害
2. **KICS の侵害**: 同じく Checkmarx のインフラコードスキャナ KICS を侵害
3. **LiteLLM の侵害**: 侵害した Trivy GitHub Action を経由して LiteLLM の CI/CD パイプラインに侵入し、PyPI 認証情報を窃取

セキュリティツール自体を攻撃ベクターに利用するという、信頼の連鎖を逆手に取った高度な手法だった。

### マルウェアの詳細

v1.82.8 には `litellm_init.pth` という悪意のある .pth ファイルが含まれており、litellm がインストールされた環境で Python プロセスが起動するたびに自動実行される。マルウェアには以下が含まれていた：

- **認証情報ハーベスター**: 環境変数や設定ファイルから API キーやクレデンシャルを収集
- **Kubernetes ラテラルムーブメントツールキット**: K8s クラスタ内での横展開を可能にする
- **永続的バックドア**: 持続的なアクセスを確保

### 影響範囲

LiteLLM は AI アプリケーション開発で広く使われる LLM ゲートウェイで、以下のプロジェクトが直接依存している：

- CrewAI、Browser-Use、Opik、DSPy、Mem0
- Instructor、Guardrails、Agno、Camel-AI

悪意のあるバージョンは UTC 10:39 から 16:00 までの約3時間公開されていた。この間に pip install でバージョン固定なしに litellm をインストールした場合、Docker イメージビルドで unpinned な litellm を含めた場合、トランジティブな依存関係で litellm が引き込まれた場合に影響を受ける可能性がある。

### 対応と検出

PyPI が約3時間でパッケージを隔離。Endor Labs、JFrog、Snyk、GitGuardian などのセキュリティベンダーが迅速に分析レポートを公開した。LiteLLM 公式もセキュリティアップデートのブログ記事を公開している。

## 今後の注目点

- TeamPCP の次のターゲット — セキュリティツールの CI/CD を狙う手法が他にも展開される可能性
- PyPI / npm などのパッケージレジストリにおけるサプライチェーン攻撃対策の強化
- CI/CD パイプラインのセキュリティ（特にサードパーティ GitHub Actions の信頼性検証）
- 影響を受けた環境でのクレデンシャルローテーションの完了状況
- SBOM（ソフトウェア部品表）と依存関係のピン留めの普及促進
