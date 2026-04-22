# CISA KEV 8 件追加と CVE-2026-40372: 連邦期限 4/23 が示すパッチ運用の現在地

- **日付**: 2026-04-23
- **カテゴリ**: Tech
- **ソース**:
  - [CISA Adds 8 Exploited Flaws to KEV — The Hacker News](https://thehackernews.com/2026/04/cisa-adds-8-exploited-flaws-to-kev-sets.html)
  - [Microsoft Patches Critical ASP.NET Core CVE-2026-40372 — The Hacker News](https://thehackernews.com/2026/04/microsoft-patches-critical-aspnet-core.html)
  - [Microsoft releases emergency patches for critical ASP.NET flaw — BleepingComputer](https://www.bleepingcomputer.com/news/microsoft/microsoft-releases-emergency-security-updates-for-critical-aspnet-flaw/)
  - [Microsoft out-of-band updates fixed critical ASP.NET Core privilege escalation flaw — Security Affairs](https://securityaffairs.com/191130/security/microsoft-out-of-band-updates-fixed-critical-asp-net-core-privilege-escalation-flaw.html)
  - [Microsoft issues out-of-band patch for critical security flaw in update to ASP.NET Core — InfoWorld](https://www.infoworld.com/article/4162194/microsoft-issues-out-of-band-patch-for-critical-security-flaw-in-update-to-asp-net-core-2.html)
  - [Known Exploited Vulnerabilities Catalog — CISA](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)

## 概要

CISA は今週、Known Exploited Vulnerabilities (KEV) カタログに 8 件の積極的悪用脆弱性を追加し、連邦機関に対して 4/23・5/4 を期限とする緊急パッチ義務を発動した。同時に Microsoft は ASP.NET Core の特権昇格欠陥 **CVE-2026-40372 (CVSS 9.1)** に対する out-of-band 修正をリリース。原因は 4/14 の Patch Tuesday で配布された .NET 10.0.6 の HMAC オフセット計算ミスで、Linux/macOS を含む全プラットフォームの ASP.NET Core クッキー・トークンの検証が信用できない状態に陥っていた。エコシステムにとっては「標準パッチ自体がインシデントの起点になる」現代的なリスクモデルを再認識させた一件。

## 詳細

### CISA KEV に追加された 8 件のうち主要な脆弱性

| CVE | 製品 | CVSS | 概要 |
|---|---|---|---|
| CVE-2025-32975 | Quest KACE Systems Management Appliance (SMA) | 10.0 | 改善された認証バイパス。リモートで管理権限取得可能。 |
| CVE-2023-27351 | PaperCut NG/MF | 8.2 | 認証バイパス。印刷管理サーバへの侵入足掛かり。 |
| CVE-2024-27199 | JetBrains TeamCity | 7.3 | 相対パストラバーサル。CI/CD パイプラインの限定管理操作。 |
| 3 件 | Cisco Catalyst SD-WAN Manager | — | アクティブ悪用が観測。SD-WAN 管理基盤の侵害につながる。 |

連邦機関への期限は 4/23・5/4 と短期。SD-WAN マネージャの侵害は分岐点でのトラフィック傍受・改竄に直結するため、即時パッチが必須。民間でも KEV はパッチ優先度の事実上のグローバル基準として機能している。

### CVE-2026-40372 — ASP.NET Core HMAC 計算欠陥

- **原因**: 4/14 Patch Tuesday の .NET 10.0.6 で、`ManagedAuthenticatedEncryptor` が HMAC の検証タグを誤ったオフセットで計算するリグレッション。`UseCustomCryptographicAlgorithms` で managed 実装を選択している環境（Linux/macOS は既定で該当）で、本来無効化されるべきクッキー・トークンが検証通過してしまう。
- **影響**: 未認証攻撃者が認証クッキーを偽造し、SYSTEM 権限相当のアクセスを取得可能。Web API・SaaS バックエンドはクリティカル。
- **修正**: ASP.NET Core 10.0.7 へアップデート。Microsoft は野生での悪用は未確認と発表。
- **発見経緯**: ユーザーから「アップデート後に復号失敗が発生する」報告が相次ぎ、Microsoft が解析の中で逆方向の問題（誤った検証通過）を確認。

### 同時期のもう一つの注目: Antigravity と Mirai

- Google のエージェント型 IDE「**Antigravity**」に、コード実行に至る脆弱性が研究者により発見された。エージェント連動 IDE の信頼境界の難しさを象徴する案件。
- D-Link DIR-823X ルータの **CVE-2025-29635** を悪用する Mirai 系ボットネットが拡大。家庭用ルータの長寿命と保守不在問題が改めて顕在化。

## 今後の注目点

- 4/23 期限を過ぎた連邦機関のコンプライアンス報告と、同期限を「事実上の業界標準」として動く民間運用の比率。
- .NET 10.0.7 へのマイグレーション混乱（コンテナイメージ・CI キャッシュ・SBOM 更新）が引き起こす副次的なダウンタイム事例。
- Microsoft 自身の SDL（Security Development Lifecycle）レビューがリグレッションをどう検出するか。Patch Tuesday の CI に対する暗号系ファジング強化の議論。
- Antigravity 級「エージェント型 IDE」の脆弱性に対するレスポンシブル・ディスクロージャの慣行整備。MCP / AGENTS.md レイヤーの信頼境界と組み合わせて議論される。
- KEV の対象拡張と、SBOM / VEX を組み合わせた「該当しない」証明を高速に出すためのツールチェーン整備。
