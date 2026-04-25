# Bitwarden CLI を襲った Shai-Hulud 系サプライチェーン攻撃の構造

- **日付**: 2026-04-26
- **カテゴリ**: Tech (Security)
- **ソース**:
  - [The Hacker News — Bitwarden CLI Compromised in Ongoing Checkmarx Supply Chain](https://thehackernews.com/2026/04/bitwarden-cli-compromised-in-ongoing.html)
  - [Socket — Bitwarden CLI Compromised in Ongoing Checkmarx Supply Chain Campaign](https://socket.dev/blog/bitwarden-cli-compromised)
  - [Bitwarden Community — Statement on Checkmarx Supply Chain Incident](https://community.bitwarden.com/t/bitwarden-statement-on-checkmarx-supply-chain-incident/96127)
  - [Techloy — Bitwarden CLI Compromised in 'Shai-Hulud' Supply Chain Attack](https://www.techloy.com/bitwarden-cli-compromised-in-shai-hulud-supply-chain-attack-334-developers-exposed/)
  - [Open Source For You — GitHub Actions Abuse Fuels Bitwarden Supply Chain Attack](https://www.opensourceforu.com/2026/04/github-actions-abuse-fuels-bitwarden-supply-chain-attack/)

## 概要

2026-04-22 の 17:57–19:30 ET（約 90 分間）、`@bitwarden/cli@2026.4.0` が悪性版として npm に流通した。Bitwarden 社は短時間で気付いて流通停止と deprecate を実施したが、この期間にインストールしたユーザーの GitHub / npm トークン、SSH 鍵、`.env`、シェル履歴、GitHub Actions / クラウドのシークレットが攻撃者管理下のドメインに流出した可能性がある。

注目すべきは、これが単独事案ではなく、Checkmarx を起点として続いている広範な npm サプライチェーン攻撃キャンペーン（Shai-Hulud と呼ばれる脅威アクター系列）の一部である点。CI/CD パイプラインそのものが「上流の上流」として狙われる構造的リスクを浮き彫りにした。

## 詳細

### 侵入経路: GitHub Actions の悪用

攻撃者は Bitwarden の CI/CD パイプライン上の GitHub Action を悪用し、リリースワークフローに悪意のあるコードを注入。これによって正規のビルド経路から `bw1.js` を含むパッケージが npm に publish された。

つまり、

- ソースコードリポジトリは改ざんされていない
- 流通したアーティファクト（npm 上の tarball）に追加ファイルが混入

という典型的なビルドタイム攻撃である。一般的な「ソースコードレビュー」では検出できない。

### マルウェアの挙動

`bw1.js` の主な動作:

1. ローカルの GitHub / npm トークン、`~/.ssh`、`.env` を収集
2. シェル履歴を読み込み、認証情報・コマンド履歴を抽出
3. GitHub Actions の `secrets` やクラウドの環境変数を収集
4. プライベートドメインに HTTP で送信、加えて GitHub commit としても外部リポジトリに push

C2 エンドポイントは Checkmarx 関連事案と同じ `audit.checkmarx[.]cx/v1/telemetry` を使用しており、技術基盤の共通性から同一系列のキャンペーンと判定されている。

### Shai-Hulud との関連

別の侵害事例では、流出データを格納する公開リポジトリ名に **「Shai-Hulud: The Third Coming」** と銘打ち、マルウェア内に **「Butlerian Jihad」マニフェスト**（フランク・ハーバート『デューン』に由来する反 AI のレトリック）を埋め込むなど、明確なイデオロギー的シグネチャを持つ脅威アクターの存在が確認されている。Checkmarx 攻撃との運用差から、

- 共通インフラを使う別オペレーター
- 元のキャンペーンから派生したスプリンターグループ

のいずれかと評価されている。Bitwarden 事案も同系列のインフラに依存している点で、Shai-Hulud キャンペーンの継続として追跡されている。

### 影響範囲

- 被害規模: 影響を受けた開発者が 334 名規模（Techloy 報告）
- エンドユーザーの Bitwarden vault データ・本番システムへの影響は確認されていない（Bitwarden 公式声明）
- ただし `bw1.js` を実行した CI / 開発者環境では、暗号資産ウォレットのキー含むあらゆる秘密情報が流出した可能性

CVE は `@bitwarden/cli@2026.4.0` に対して採番中。

### 推奨対応

Socket / Bitwarden が共通して推奨する対策:

1. `@bitwarden/cli@2026.4.0` を直ちに削除
2. `@bitwarden/cli@2026.3.0` へのダウングレード、もしくは Bitwarden 公式の署名付きバイナリへの切替
3. **GitHub PAT、npm トークン、SSH 鍵、クラウドの API キー、`.env` 内のシークレットをすべてローテーション**
4. 自身のアカウント配下に身に覚えのない新規リポジトリが作られていないか監査
5. トークンスコープの最小化と、短命なクレデンシャル（OIDC ベース、短時間 TTL）への移行

## 今後の注目点

- **CI/CD への信頼境界の引き直し**: GitHub Actions / GitLab CI のワークフロー権限分離、Reusable Workflow の署名強制、`workflow_run` トリガーの審査強化が必要。
- **npm publish の保証強化**: npm の Provenance / Sigstore / Trusted Publisher の導入率を上げ、CI から直接 publish するときに署名アーティファクトを必須化する流れが加速する見込み。
- **Shai-Hulud キャンペーンの継続性**: Checkmarx → Bitwarden と続いた連鎖が、次にどの開発者向けツール（パスワードマネージャ、CLI、SDK）に波及するか。
- **暗号資産業界への影響**: Bitwarden CLI を使うウォレット運用者が多く、流出鍵を悪用した暗号資産盗難の追跡が今後の重要指標。
- **検出手法の発展**: Socket・Snyk・Aikido 等のサプライチェーン監視ツールが「インストール後 90 分以内の悪性版」を検知できるかが試される事案。tarball 差分ベースの自動検知が必要。
