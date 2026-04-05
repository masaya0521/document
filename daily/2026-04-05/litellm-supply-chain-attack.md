# LiteLLM サプライチェーン攻撃 — AIインフラの新たな脅威

- **日付**: 2026-04-05
- **カテゴリ**: Tech
- **ソース**: [InfoQ](https://www.infoq.com/news/2026/03/litellm-supply-chain-attack/), [HeroDevs](https://www.herodevs.com/blog-posts/the-litellm-supply-chain-attack-what-happened-why-it-matters-and-what-to-do-next), [Sonatype](https://www.sonatype.com/blog/compromised-litellm-pypi-package-delivers-multi-stage-credential-stealer)

## 概要

2026年3月24日、AIインフラの人気ライブラリ LiteLLM の PyPI パッケージ（v1.82.7 / v1.82.8）がサプライチェーン攻撃により侵害された。約40分間の配布で、SSH鍵・クラウドクレデンシャル・APIトークンなどを窃取するマルウェアが拡散。LiteLLM はクラウド環境の約36%に存在するため、影響範囲は極めて広い。

## 詳細

### 攻撃の経緯

攻撃は TeamPCP と呼ばれる脅威グループによるもの。攻撃チェーンは以下の通り:

1. **Trivy の CI/CD アクション侵害**: LiteLLM のセキュリティスキャンに使われていた `trivy-action` GitHub Action が侵害された
2. **PyPI トークン窃取**: 侵害された Trivy Action 経由で LiteLLM の PyPI パブリッシングトークンが外部に送信された
3. **悪意あるパッケージ公開**: 窃取したトークンを使い、クレデンシャルスティーラーを仕込んだ v1.82.7 / v1.82.8 が PyPI に公開された
4. **データ窃取**: インストールされたパッケージは `litellm_init.pth` 経由で起動し、以下を収集・暗号化して外部送信:
   - SSH 鍵
   - AWS / GCP / Azure クレデンシャル
   - Kubernetes シークレット
   - `.env` ファイル
   - データベース設定

### 影響の規模

- LiteLLM の1日あたりのダウンロード数は約340万
- 約40分間の公開だったが、自動デプロイパイプラインによる被害が懸念される
- クラウド環境の約36%に LiteLLM が存在
- 窃取データは `models.litellm.cloud`（非公式ドメイン）にPOSTで送信された

### 対応

- PyPI が約40分後にパッケージを隔離
- LiteLLM チームが v1.83.0 をクリーンな CI/CD v2 パイプラインから安全にリリース
- 新パイプラインでは隔離環境・強化されたセキュリティゲート・リリース分離を導入

### 教訓

この攻撃は、AI開発エコシステムにおけるサプライチェーンセキュリティの脆弱性を浮き彫りにした:

- **CI/CD 依存関係の信頼性**: セキュリティスキャンツール自体が攻撃経路になり得る
- **自動デプロイのリスク**: `pip install --upgrade` を自動実行するパイプラインは短時間の侵害でも被害を受ける
- **AI インフラの集中リスク**: LiteLLM のように広く使われるAIゲートウェイは高価値ターゲットとなる

## 今後の注目点

- TeamPCP による他のパッケージへの攻撃の可能性（同グループはEU委員会クラウドハックにも関与）
- PyPI やnpm等のパッケージレジストリにおけるパブリッシングトークンのセキュリティ強化策
- AI開発向けのサプライチェーンセキュリティベストプラクティスの策定
- Sigstore / SLSA 等のソフトウェアサプライチェーン署名・検証の採用加速
