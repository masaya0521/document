# GlassWorm Open VSX サプライチェーン攻撃の拡大

- **日付**: 2026-04-27
- **カテゴリ**: Tech
- **ソース**: [The Hacker News](https://thehackernews.com/2026/03/glassworm-supply-chain-attack-abuses-72.html), [Cyber Security News](https://cybersecuritynews.com/73-open-vsx-sleeper-extensions-linked-to-glassworm-malware/), [Socket](https://socket.dev/blog/73-open-vsx-sleeper-extensions-glassworm), [CSO Online](https://www.csoonline.com/article/4145579/open-vsx-extensions-hijacked-glassworm-malware-spreads-via-dependency-abuse.html)

## 概要

VS Code 互換のオープン拡張機能マーケットプレイス Open VSX を狙った GlassWorm キャンペーンが、新たに73本の「スリーパー拡張」を追加で配布していたことが明らかになった。1月末からの累計で 145 本超が GlassWorm に関連付けられ、開発者環境を直接侵害するサプライチェーン攻撃として2026年最大級のインシデントに発展している。すでに6拡張がペイロードを起動済みで、被害は VS Code、Cursor、Windsurf、Google Antigravity など Open VSX を採用する派生 IDE 全体に及ぶ。

## 詳細

### スリーパー拡張という戦術

スリーパー拡張は「公開時は無害なまま放置し、信頼とインストール数を稼いでから後続アップデートで初めて武器化する」ハイブリッド型の供給網攻撃である。リリース直後はマーケットプレイスのレビュー、SAST、シグネチャベースのスキャナーをすり抜けやすく、開発者がレビュー時に確認した内容と「実行時に展開されるコード」が乖離していく点が特徴。

### extensionPack/extensionDependencies の悪用

Socket の分析によると、攻撃者はこれまでの直接的な悪意コード混入から、`extensionPack` および `extensionDependencies` を介した間接配信へと手口を進化させている。当初は単独で見える拡張が、後のバージョンアップで GlassWorm 関連の別拡張を依存ツリー経由で引き込むよう書き換えられる。これにより:

- マーケットプレイス側のスキャンは「親拡張」だけを見て依存先の追加を見逃しやすい
- 既にインストールしているユーザーには、IDE 起動時に依存解決の延長で勝手に悪性拡張が引き込まれる
- 削除しても親拡張が再度依存を呼び戻すため、根本除去には依存ツリー全体の追跡が必要

### ターゲットの広域化

73拡張の多くは linter、formatter、code runner、AI コーディング補助(Claude Code・Google Antigravity 連携など)といった「日常的に常駐するツール」を模倣している。すなわち、ターミナルセッション・GitHub トークン・クラウド資格情報・LLM API キーを収集する設計と整合しており、開発者ノード経由で本番系へ横展開する典型的な supply chain 攻撃モデルと一致する。

### 関連事案: Bitwarden CLI も Checkmarx ルートで侵害

同時期に Bitwarden CLI が、Checkmarx の依存パッケージ侵害を起点に汚染された事例も判明している。GlassWorm 単体の問題というより、開発者ツールチェーン全体に対する複合的な攻撃シーズンであることが示唆される。

## 今後の注目点

- **Open VSX のガバナンス強化**: Eclipse Foundation/Open VSX 運営側の即時テイクダウンと、依存先メタデータのスキャン強化が進むか。VS Code Marketplace との比較で監視能力に差が出ている点が業界課題。
- **IDE 派生プロダクトのリスク連鎖**: VS Code Insiders 以外で Open VSX を採用する Cursor・Windsurf・Antigravity など AI コーディング系 IDE は同根のリスクを抱える。各社のレジストリ切替・差し戻し方針を要確認。
- **拡張機能のロックファイル化**: npm の `package-lock.json` 相当の「拡張バージョン固定+依存ツリーフリーズ」が IDE 標準機能として議論される可能性。
- **企業環境でのプライベートレジストリ採用加速**: 監査済みミラーや allowlist によるホワイトリスト制への移行が、GitHub Copilot Enterprise・Cursor Enterprise 等で標準化されるか。
- **AI コーディングツール依存パスの可視化**: Claude Code・Antigravity など LLM 連携拡張は資格情報・履歴へのアクセス権が広いため、被害インパクトが従来の拡張より高い。攻撃者がこの層に集中する傾向は今後も続くと見られる。
