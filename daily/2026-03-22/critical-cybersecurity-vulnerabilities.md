# 重大サイバーセキュリティ脆弱性の連鎖 — SharePoint と Chrome ゼロデイ

- **日付**: 2026-03-22
- **カテゴリ**: Tech
- **ソース**: [Help Net Security](https://www.helpnetsecurity.com/2026/03/19/sharepoint-vulnerability-cve-2026-20963-exploited/), [SOC Prime](https://socprime.com/blog/cve-2026-3910-vulnerability/), [The Hacker News](https://thehackernews.com/2026/03/google-fixes-two-chrome-zero-days.html)

## 概要

2026年3月、エンタープライズ環境を脅かす2つの重大な脆弱性が同時に悪用されている。Microsoft SharePoint のデシリアライゼーション脆弱性（CVE-2026-20963, CVSS 9.8）と Google Chrome V8 エンジンのゼロデイ（CVE-2026-3910, CVSS 8.8）は、いずれも CISA の Known Exploited Vulnerabilities（KEV）カタログに追加され、連邦機関に緊急パッチ適用が義務付けられた。

## 詳細

### CVE-2026-20963: SharePoint デシリアライゼーション RCE

**深刻度**: CVSS 9.8（Critical）

SharePoint の信頼されていないデータのデシリアライゼーション処理に起因する脆弱性。攻撃者は特別に細工したデータパケットをネットワーク経由で脆弱なサーバーに送信するだけで、認証なし・ユーザー操作なしでリモートコード実行が可能。

**影響を受けるバージョン**:
- SharePoint Enterprise Server 2016
- SharePoint Server 2019
- SharePoint Server Subscription Edition
- SharePoint Server 2007/2010/2013（サポート終了済みだが脆弱）

**タイムライン**:
- 2026年1月: Microsoft がパッチを公開
- 2026年3月18日: CISA が KEV カタログに追加、積極的な悪用を確認
- 2026年3月21日: 連邦機関向け修正期限

パッチ公開から約2ヶ月が経過しても未適用の環境が標的となっている。攻撃者グループは特定されていないが、APT（Advanced Persistent Threat）による組織的な悪用が疑われている。

### CVE-2026-3910: Chrome V8 Maglev コンパイラの型混同

**深刻度**: CVSS 8.8（High）

Chrome の JavaScript/WebAssembly エンジン V8 の Maglev コンパイラにおける型混同（Type Confusion）脆弱性。Maglev コンパイラの Phi untagging パス（「タグ付き」JavaScript 値を「タグなし」の生のマシン型に変換する最適化処理）にロジックエラーがあり、細工された HTML ページを通じてブラウザサンドボックス内で任意のコード実行が可能。

**もう1つのゼロデイ**: CVE-2026-3909（Skia グラフィックライブラリの脆弱性、CVSS 8.8）も同時に修正されている。

**タイムライン**:
- 2026年3月10日: Google が内部で発見・報告
- 2026年3月13日: 緊急パッチ（Chrome 146.0.7680.75/76）を公開
- 2026年3月27日: 連邦機関向け修正期限

### 共通する課題

両脆弱性に共通するのは「パッチギャップ」の問題。パッチが利用可能であるにもかかわらず、適用が遅れた環境が攻撃されている。特にエンタープライズ環境では、互換性テストやダウンタイムの制約により、パッチ適用が数週間から数ヶ月遅れることが多い。

## 今後の注目点

- **SharePoint 攻撃の帰属**: 未特定の攻撃者グループの正体が判明するか。国家支援型 APT の可能性
- **Chrome ゼロデイの攻撃チェーン詳細**: Google が技術詳細を公開していないため、サンドボックスエスケープと組み合わせた攻撃の全容が不明
- **パッチ管理の再考**: 特に地政学的緊張が高まる中、国家支援型攻撃のリスクが増大しており、パッチ適用の迅速化が急務
- **CISA KEV カタログの影響力**: 連邦機関以外の民間企業にも KEV カタログベースのパッチ管理が広がるか
