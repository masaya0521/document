# VS Code ゼロデイ：ワンクリックで GitHub トークンを奪う Webview の落とし穴

- **日付**: 2026-06-06
- **カテゴリ**: Tech
- **ソース**: [The Hacker News](https://thehackernews.com/2026/06/one-click-github-dev-attack-lets.html) / [BleepingComputer](https://www.bleepingcomputer.com/news/security/vs-code-zero-day-lets-hackers-steal-github-tokens-in-one-click/) / [SecurityWeek](https://www.securityweek.com/vs-code-vulnerability-allows-one-click-github-token-theft/)

## 概要

Visual Studio Code に、ワンクリックで GitHub OAuth トークンを窃取できるゼロデイ脆弱性が公表された。攻撃者が用意した悪意ある Jupyter Notebook へのリンクを被害者がクリックするだけで、トークンが奪われ、private を含む全リポジトリへの読み書きが可能になる。

トリガー条件はリンクのクリックのみ。ユーザーが特別な操作をしなくても被害が成立する点で深刻度が高い。

## 詳細

### 攻撃メカニズム

本脆弱性は、VS Code のメインウィンドウと Webview 間のメッセージパッシング機構を悪用する。攻撃の流れは以下の通り。

1. 攻撃者が細工した Jupyter Notebook を用意する。
2. 信頼されない Webview 内で悪意ある JavaScript を実行し、メインエディタ側のキー入力をシミュレートする。
3. `Ctrl+Shift+P` をトリガーしてコマンドパレットを開く。
4. 攻撃者が管理する拡張機能をインストールさせる。
5. その拡張機能が GitHub.dev に渡される GitHub OAuth トークンを抽出。
6. GitHub API を叩いて被害者がアクセスできる全 private リポジトリを列挙する。

Webview から本来は隔離されているはずのメインウィンドウへ「キー入力の擬似注入」ができてしまう点が本質的な欠陥といえる。

### 影響

奪われたトークンは、被害者がアクセスできる全リポジトリ（private 含む）への完全な読み書き権限を持つ。企業の内部リポジトリ大量流出につながりうる。

### 開示と対応

- 研究者は GitHub への通知の **1時間後** に詳細を公開した（MSRC を通さない実質的なフルディスクロージャ）。
- 記事公開後、Microsoft は「本問題はサービス側で緩和済み、顧客側の対応は不要」と The Hacker News に回答。
- ただしデスクトップ版は未パッチのままとみられている。

## 今後の注目点

- デスクトップ版 VS Code への正式パッチ提供タイミング。
- Webview とメインウィンドウ間のメッセージ境界に関する根本的な設計見直しが入るか。
- 同様のキー入力擬似注入が他の Electron ベース IDE/エディタにも波及しないか。
- 短時間フルディスクロージャの是非をめぐる脆弱性開示プロセスの議論。
