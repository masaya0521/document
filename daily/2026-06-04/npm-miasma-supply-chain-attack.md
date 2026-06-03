# npm サプライチェーン攻撃「Miasma」と Shai-Hulud の系譜

- **日付**: 2026-06-04
- **カテゴリ**: Tech
- **ソース**: [The Hacker News](https://thehackernews.com/) / [Cybertechnology Insights](https://cybertechnologyinsights.com/daily-roundup/daily-cybertech-highlights-essential-news-and-analysis-3-june-2026/)

## 概要

Red Hat の `@redhat-cloud-services` 名前空間配下で公開されていた 30 を超える npm パッケージが侵害され、認証情報窃取マルウェア Shai-Hulud の新変種「Miasma」を配布していたことが判明した。著名なベンダー名前空間が侵害された点で、エコシステム全体への信頼を揺るがすサプライチェーン攻撃となっている。

## 詳細

### 攻撃の手口

侵害されたパッケージはインストール時（postinstall 等のライフサイクルスクリプトが典型的な経路）に Miasma を実行し、開発者・CI 環境の認証情報（npm トークン、クラウドの API キー、環境変数等）を窃取するとみられる。窃取した認証情報を使ってさらに別パッケージへ自己増殖的に侵害を広げる挙動が Shai-Hulud 系列の特徴であり、ワーム的に拡散するリスクがある。

### Shai-Hulud の系譜

Shai-Hulud は npm エコシステムを標的とする認証情報窃取マルウェアのファミリーで、今回の「Miasma」はその新変種に位置づけられる。著名な公式名前空間（ここでは Red Hat の Cloud Services）が踏み台になることで、依存関係を通じて下流の多数のプロジェクトへ波及する恐れがある。

### 同時期の他の脅威

- **WeedHack**: Minecraft プレイヤーを標的とする大規模マルウェアキャンペーン。1 月以降 116,000 台超に感染。
- **Grindr の情報漏洩疑惑**: パスワードと位置情報が流出した疑い。
- **Dashlane / Instagram のアカウント乗っ取り**: ブルートフォースや AI サポートツールを欺く手口でのアカウント侵害が報告。

## 今後の注目点

- 侵害された具体的なパッケージ名・バージョンと、影響を受けた下流プロジェクトの特定
- npm / Red Hat 側の対応（パッケージ削除、トークン無効化、2FA 強制等）
- postinstall スクリプトを悪用する攻撃に対する防御策（`--ignore-scripts`、lockfile 固定、SBOM、依存の最小化）の再評価
- Shai-Hulud ファミリーの今後の変種と、公式名前空間を狙う攻撃トレンドの継続性
