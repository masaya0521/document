# Red Hat npm 供給網攻撃「Miasma」— 認証情報窃取ワームの新亜種

- **日付**: 2026-06-03
- **カテゴリ**: Tech
- **ソース**: [Red Hat RHSB-2026-006](https://access.redhat.com/security/vulnerabilities/RHSB-2026-006) / [The Hacker News](https://thehackernews.com/2026/06/miasma-supply-chain-attack-compromises.html) / [Wiz Blog](https://www.wiz.io/blog/miasma-supply-chain-attack-targeting-redhat-npm-packages) / [StepSecurity](https://www.stepsecurity.io/blog/multiple-redhat-cloud-services-npm-packages-compromised)

## 概要

2026年6月1日、`@redhat-cloud-services` npm スコープ配下の複数パッケージが供給網汚染を受けていたことが公表された。32個の公式パッケージが、インストール時に自動実行される認証情報窃取ワームに汚染されていた。

このキャンペーンは「Miasma: The Spreading Blight」と名付けられ、過去に脅威アクター TeamPCP と関連付けられた「Mini Shai-Hulud」マルウェアファミリの新亜種とされる。汚染されたパッケージ群は週あたり累計約8万ダウンロードに達していた。

## 詳細

### 攻撃の経緯

侵害された GitHub アカウントが、Red Hat の GitHub 組織で管理されるパッケージに悪意あるコードを注入するために使われた。少なくとも32のパッケージリリースが、対応するソースリポジトリと一致しない不正な改変を含んでいた。

### ペイロードの挙動

ペイロードは多段階の認証情報ハーベスタで、以下の広範なシークレットを収集する。

- GitHub Actions のシークレット
- AWS / GCP / Azure のクラウド認証情報
- Kubernetes トークン
- HashiCorp Vault のトークン
- npm / CircleCI のトークン

さらに検出回避が作り込まれており、StepSecurity の Harden-Runner を明示的にバイパスしようとする挙動まで含まれていた。「ワーム」と称される通り、窃取した認証情報を使って他のパッケージ・リポジトリへ感染を広げる自己増殖性を備える点が特徴。

### Shai-Hulud 系譜

本攻撃は2025年以降 npm エコシステムを繰り返し襲ってきた Shai-Hulud 系ワームの流れを汲む。インストールスクリプト（postinstall 等）を悪用し、開発者のマシンや CI 環境のシークレットを横取りして連鎖的に拡散する手口は、近年のサプライチェーン攻撃の典型パターンとなりつつある。

### Red Hat の対応と影響範囲

Red Hat はエンジニアリングチームが公開後に汚染バージョンを npm から削除した。重要な点として、Red Hat 製品やエンタープライズソフトウェアは汚染バージョンでビルド・出荷されていないことを確認している。エンジニアリングチームによるバージョン固定（version pinning）が製品への混入を防いだ。

つまり被害が及び得るのは、汚染期間中に該当パッケージを直接インストールした個人開発者・CI 環境であり、Red Hat 製品の利用者ではない。

## 今後の注目点

- インストールスクリプト実行のデフォルト無効化（`--ignore-scripts`）や、信頼できるパブリッシュ経路（npm provenance / Sigstore）の普及が進むか
- 大手ベンダーの公式 npm スコープすら侵害され得るという前提でのゼロトラスト設計
- 汚染期間中に CI でインストールした組織のトークンローテーション・侵害調査
- npm エコシステムにおける Shai-Hulud 系ワームの継続的進化と、レジストリ側の防御強化
- メンテナアカウントの保護（フィッシング耐性のある MFA、最小権限のパブリッシュトークン）
