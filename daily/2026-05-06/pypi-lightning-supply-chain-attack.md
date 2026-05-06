# PyTorch Lightning サプライチェーン攻撃の解剖

- **日付**: 2026-05-06
- **カテゴリ**: Tech
- **ソース**: [BleepingComputer](https://www.bleepingcomputer.com/news/security/backdoored-pytorch-lightning-package-drops-credential-stealer/) / [Semgrep](https://semgrep.dev/blog/2026/malicious-dependency-in-pytorch-lightning-used-for-ai-training/) / [Socket](https://socket.dev/blog/lightning-pypi-package-compromised) / [The Hacker News](https://thehackernews.com/2026/04/pytorch-lightning-compromised-in-pypi.html)

## 概要

PyTorch Lightning は AI モデル学習で広く使われるラッパーライブラリで、PyPI における月間ダウンロード数は数千万規模にのぼる。2026 年 4 月 30 日に公開された 2.6.2 と 2.6.3 のバージョンに、Mini Shai-Hulud と呼ばれる系統の認証情報窃取マルウェアが混入していたことが、Socket Research Team によって公開後 18 分で検出された。同日中に PyPI 管理者がパッケージを quarantine し、PyTorch Lightning は 2.6.1 を再公開して安全な参照先に巻き戻している。

直近で広範囲に流通した npm の Shai-Hulud キャンペーンを Python 側へ持ち込んだ初の事例とみられ、AI 学習基盤を狙うサプライチェーン攻撃が「実用段階」に入ったことを示す。

## 詳細

### 感染チェーン

import 時点でユーザー操作なしに以下が走る:

1. パッケージ初期化フック内で `bun` (v1.3.13) ランタイムを GitHub から動的にダウンロード。
2. 11.4 MB に及ぶ強難読化 JavaScript ペイロード `router_runtime.js` をバックグラウンドで実行。
3. 開発者ホスト上の各種シークレットを列挙して送出。

ステージドペイロードを Bun で走らせる構造により、Python の静的解析・SCA ツールでは検出が遅れやすい。

### 流出対象

- GitHub / npm のアクセストークン
- SSH 秘密鍵
- AWS / GCP / Azure 認証情報
- Kubernetes kubeconfig、Vault トークン
- Docker レジストリ認証
- `.env` ファイル全般
- 暗号資産ウォレット
- CI ランナー上の各種シークレット

「AI/MLOps 開発者の権限の高さ」が実害の大きさを増幅させている点が今回の本質。AI 学習基盤を握るアカウントは、GPU 群の管理権限・モデル重みストレージ・社内データレイクへの広範な R/W を併せ持つことが多く、波及範囲はモデルの「重み窃取」「学習データ汚染」まで広がりうる。

### 攻撃者の戦術

Socket と Semgrep の解析によれば、攻撃者は GitHub Actions など CI 経由で取得したメンテナトークンを通じて公開権限を奪取した可能性が高い。Mini Shai-Hulud 系は元の Shai-Hulud 同様、感染端末から見つけたトークンで他パッケージを汚染しに行くワーム的設計を持つ。

### Lightning AI / PyTorch コミュニティの初動

- 2.6.1 を「最新安全版」として PyPI に再公開
- 2.6.2 / 2.6.3 を quarantine
- 公式 GitHub Issue で「2.6.2 / 2.6.3 を import した環境はすべて compromise 済みとして扱え」と警告
- 配布署名・SBOM・トラステッドパブリッシングの全面適用に向けた議論を再点火

## 今後の注目点

- **AI ライブラリへの SLSA / Sigstore 強制適用**: モデル学習エコシステムは依存関係が深く、暗黙の信頼が大きい。今回のインシデントを契機に、署名・トラステッドパブリッシング義務化の議論が一段加速する見込み。
- **「import-time 実行」の根絶**: Python パッケージング全体で副作用つき import を許してきた歴史的負債がリスクの根源にある。`pyproject.toml` ベースで実行を遅延させる規約づくりが今後の焦点。
- **MLOps シークレット最小化**: AI 学習用ノードの権限を CI と同じく最小化する運用への移行が必要。学習用クラウド権限を短命トークン化する基盤（OIDC ベースのフェデレーション）採用が広がる可能性。
- **Mini Shai-Hulud 系の横展開**: npm 起源だったキャンペーンが PyPI に渡った以上、次は Maven Central / RubyGems / NuGet など他のレジストリにも波及する公算。各エコシステムでの quarantine 体制が試される。
- **AI 学習データへの間接攻撃**: 認証情報奪取の先で、学習データ・チェックポイントの改ざん（モデルポイズニング）に発展するシナリオは、今回のような MLOps チェーン汚染で初めて現実的になる。
