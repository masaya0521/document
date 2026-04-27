# Bitwarden CLI 改ざん事件：Checkmarx 連鎖を狙った供給チェーン攻撃の詳細

- **日付**: 2026-04-22 発生 / 2026-04-28 Daily Digest
- **カテゴリ**: Tech (Security)
- **主なソース**:
  - [The Hacker News — Bitwarden CLI Compromised in Ongoing Checkmarx Supply Chain Campaign](https://thehackernews.com/2026/04/bitwarden-cli-compromised-in-ongoing.html)
  - [Bitwarden Community — Statement on Checkmarx Supply Chain Incident](https://community.bitwarden.com/t/bitwarden-statement-on-checkmarx-supply-chain-incident/96127)
  - [Socket — Bitwarden CLI Compromised](https://socket.dev/blog/bitwarden-cli-compromised)
  - [Sophos — Supply chain attacks hit Checkmarx and Bitwarden developer tools](https://www.sophos.com/en-us/blog/supply-chain-attacks-hit-checkmarx-and-bitwarden-developer-tools)
  - [Cremit — Inside the Bitwarden CLI Supply Chain Attack: 90 Minutes That Compromised Developer Secrets](https://www.cremit.io/blog/bitwarden-cli-supply-chain-attack-april-2026)
  - [SecurityWeek — Bitwarden NPM Package Hit in Supply Chain Attack](https://www.securityweek.com/bitwarden-npm-package-hit-in-supply-chain-attack/)

## 概要

2026-04-22 17:57 〜 19:30 ET の **約 90 分間**、`@bitwarden/cli@2026.4.0` の npm 配布パッケージに、開発者の認証情報を窃取するマルウェアが混入していた。攻撃は同時期に進行していた Checkmarx 関連の供給チェーンキャンペーンの一部と判断されており、Bitwarden は CI/CD パイプライン内で **GitHub Action のサプライチェーンが侵害された** ことが侵入経路だったとしている。Bitwarden CLI は 1,000 万ユーザー超が利用するパスワードマネージャの開発者向けインターフェースであり、今回の攻撃で **334 人の開発者** のシークレットが流出した可能性がある。

ベンダーは「エンドユーザーの vault データへのアクセスは確認されていない」と明言しているが、攻撃の規模・手法は npm エコシステムに対する継続的な supply chain 攻撃として極めて重要な事例。

## 詳細

### 1. タイムライン

- 2026-04-22 17:57 ET: 改ざん版 `@bitwarden/cli@2026.4.0` が npm に公開
- 2026-04-22 19:30 ET: Bitwarden が異常を検知し、改ざん版を npm から取り下げ
- 2026-04-23 以降: Bitwarden および Socket / The Hacker News が技術詳細を公開
- 2026-04-25 週: Sophos / SecurityWeek 等が campaign 全体のレポートを発表

### 2. 攻撃ベクター

- 侵害対象は **Bitwarden の CI/CD で利用していた GitHub Action**。攻撃者はこの Action を経由してパッケージビルド時にコードを注入。
- 同時期に複数のリポジトリで類似の侵害が観測されており、**TeamPCP (Checkmarx 攻撃を主張)** と **Shai-Hulud worm 派生**との関連が指摘されている。
- 攻撃に使われたインフラは `audit.checkmarx[.]cx` という Checkmarx の正規ドメインに見せかけたタイポスクワッティング。

### 3. ペイロードの動作

- マルウェアは `bw1.js` というファイルに格納され、**npm の `preinstall` フック** から実行。
- 窃取対象は次のとおり広範:
  - GitHub / npm のアクセストークン
  - `~/.ssh` 配下の SSH 鍵
  - `.env` ファイル
  - シェル履歴 (`.bash_history`, `.zsh_history`)
  - GitHub Actions のシークレット
  - クラウドプロバイダの認証情報 (AWS / GCP / Azure)
- 収集データは AES-256-GCM で暗号化し、`audit.checkmarx[.]cx` へ送信。攻撃者がログ解析される可能性を低減する設計。

### 4. 影響範囲

- Cremit / Socket の解析では **約 334 人の開発者** が改ざん版を取得・実行した可能性。
- 主な被害想定:
  - 個人開発者のローカル環境のシークレット漏洩
  - CI/CD でこのパッケージを使っていた組織の secrets 漏洩
  - 連鎖的に侵害先のリポジトリが乗っ取られる worm 拡散リスク
- Bitwarden は **エンドユーザーの vault データへのアクセスは確認されていない** と発表。CLI のロジック自体には変更がなく、利用者の認証情報を直接読み取るコードは含まれていなかったため。

### 5. 推奨対応

- 影響期間中に `npm install -g @bitwarden/cli@2026.4.0` を実行した環境では:
  - GitHub / npm トークンのローテーション
  - SSH 鍵の再発行
  - クラウド IAM 認証情報の更新
  - `.env` の機密値 (DB パスワード, API キー) の差し替え
- CI/CD パイプラインで preinstall フックを禁止する `npm install --ignore-scripts` の検討
- npm パッケージの依存先に対する **provenance 検証** (`npm audit signatures`) の有効化
- GitHub Actions のサードパーティアクションを **commit SHA で固定** する運用への切替

### 6. 業界への含意

- **2025 年から続く Shai-Hulud worm 系列の継続性**: 過去 1 年で nx, qix-related, eslint-config-prettier など複数の高人気パッケージが侵害されており、攻撃インフラは進化を続けている。
- **「正規ドメインに似せた C2」**は、ロギング / EDR の運用ですり抜けやすい点で防御が難しい。SOC / DevSecOps は許可ドメインリストの精査が必要。
- **GitHub Action の信頼境界** が改めて課題に。Reusable workflow / pinned action / OIDC の運用整備が急務。
- ベンダー視点では、Bitwarden のように 90 分以内で検知・取り下げできた対応スピードが被害規模を抑えた要因。**out-of-band な monitoring** (Socket 等の外部サービス) の価値が再確認される。

## 今後の注目点

- TeamPCP と Shai-Hulud worm の関連性、そして次の標的パッケージ
- npm registry 側の防御策アップデート (provenance enforced 化、preinstall hook 制限の議論)
- GitHub Actions 経由の侵害が継続するか — Bitwarden で侵害された具体的な Action と、その他の利用者への影響
- Checkmarx 自身の侵害事案の最終報告とフォレンジック結果
- 影響を受けた 334 人の開発者の組織への二次被害が発生するか (横展開リスク)
- CISA / 各国 CERT が npm エコシステム向けに新しい advisory / mitigation を出すか
