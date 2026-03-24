# GitHub Actions サプライチェーン攻撃 — Trivy/Checkmarx 侵害の全容

- **日付**: 2026-03-25
- **カテゴリ**: Tech
- **ソース**: [The Hacker News](https://thehackernews.com/2026/03/trivy-security-scanner-github-actions.html)

## 概要

2026年3月19日、脅威アクター「TeamPCP」が Aqua Security の脆弱性スキャナー Trivy の GitHub Actions を侵害した。攻撃は Checkmarx の GitHub Actions にも波及し、CI/CD パイプラインから認証情報を大規模に窃取するサプライチェーン攻撃に発展した。CVE-2026-33634（CVSS 9.4）として追跡されている。

## 詳細

### 攻撃の手法

攻撃者は `aquasecurity/trivy-action` リポジトリの76バージョンタグのうち75を force-push で改竄した。信頼されたバージョン参照を、情報窃取マルウェアの配布メカニズムに変換するという手口である。

改竄は以下の4つのリポジトリに拡大した:
- `aquasecurity/trivy-action`
- `aquasecurity/setup-trivy`
- `Checkmarx/kics-github-action`
- `Checkmarx/ast-github-action`

合計110以上のバージョンタグが改竄され、三段階のクレデンシャルスティーラーを含む悪意のあるコミットに置き換えられた。

### 被害の連鎖

1. **第一段階**: GitHub Actions のバージョンタグ改竄により、CI/CD パイプラインで実行されるワークフローに悪意のあるコードを注入
2. **第二段階**: 窃取された認証情報を利用して npm パッケージを侵害し、自己増殖型ワーム（CanisterWorm）を配布
3. **第三段階**: Kubernetes ワイパーの展開と、Aqua Security 内部リポジトリの改竄

### 攻撃者について

TeamPCP は2025年から2026年にかけて活動するクラウドネイティブ特化の脅威アクターで、以下の別名でも知られる:
- DeadCatx3
- PCPcat
- ShellForce
- CanisterWorm

Wiz と Aikido の両社が Trivy 侵害を TeamPCP の仕業と特定している。

### 影響範囲

Trivy は最も広く使われているオープンソース脆弱性スキャナーの一つであり、多数の企業の CI/CD パイプラインに組み込まれている。バージョンタグを固定してピン留めしていたプロジェクトも、force-push によりタグ自体が改竄されたため影響を受けた。

## 今後の注目点

- **npm パッケージの侵害範囲**: CanisterWorm による二次被害の全容がまだ明らかになっていない
- **GitHub Actions のセキュリティモデル**: バージョンタグではなくコミット SHA でのピン留めがベストプラクティスとして再認識される
- **サプライチェーンセキュリティの制度化**: SLSA や Sigstore などのソフトウェアサプライチェーンセキュリティフレームワークの採用加速が予想される
- **TeamPCP の次の標的**: クラウドネイティブエコシステムの他のツールチェーンへの攻撃拡大の可能性
