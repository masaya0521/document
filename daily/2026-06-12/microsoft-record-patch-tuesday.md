# Microsoft 史上最大の Patch Tuesday — 200 件修正とワーム化可能な TCP/IP 脆弱性

- **日付**: 2026-06-12
- **カテゴリ**: Tech
- **ソース**: [BleepingComputer](https://www.bleepingcomputer.com/news/microsoft/microsoft-june-2026-patch-tuesday-fixes-3-zero-day-200-flaws/amp/) / [Zero Day Initiative](https://www.zerodayinitiative.com/blog/2026/6/9/the-june-2026-security-update-review) / [Tenable](https://www.tenable.com/blog/microsofts-june-2026-patch-tuesday-addresses-198-cves-cve-2026-49160-cve-2026-50507)

## 概要

Microsoft は 2026 年 6 月 9 日の月例セキュリティ更新（Patch Tuesday）で約 200 件（ソースにより 198〜208 件）の脆弱性を修正した。2003 年の Patch Tuesday 開始以来、単月としては**史上最大**の規模。Critical 33 件（うち RCE 28 件）、公開済みゼロデイ 3 件、活発に悪用されている脆弱性 1 件を含む。

特にワーム化可能な TCP/IP カーネル RCE（CVSS 9.8）が含まれており、企業環境では優先度の高い適用が求められる。修正直後に Defender の新たなゼロデイエクスプロイト「RoguePlanet」が公開されるなど、パッチ適用後も予断を許さない状況が続いている。

## 詳細

### 公開済みゼロデイ（3 件）

| CVE | 内容 |
|-----|------|
| CVE-2026-45586 | Windows Collaborative Translation Framework (CTFMON) の権限昇格。認証済み攻撃者がローカルで権限を昇格可能 |
| CVE-2026-49160 | HTTP.sys の DoS。通称「HTTP/2 Bomb」。HTTP/2 のヘッダ圧縮処理を悪用し、ごく少量のデータでサーバに不均衡に大きなメモリ割り当てを強制する |
| CVE-2026-50507 | BitLocker のセキュリティ機能バイパス。物理アクセスを持つ攻撃者が保護を回避可能 |

### 特に危険な脆弱性

- **CVE-2026-45657**(CVSS 9.8): カーネルの TCP/IP 処理に起因する、未認証リモートからの SYSTEM 権限コード実行。**ワーム化可能**とされ、今回の更新で最も優先度が高い。
- **CVE-2026-41091**: Microsoft Defender の権限昇格。**実際に悪用が確認されている**（in the wild)。複数の研究者が独立に報告しており、悪用の広がりが示唆される。

### パッチ公開直後の動き

- 修正からわずか数時間後、研究者が Defender の新ゼロデイエクスプロイト「**RoguePlanet**」を公開。Defender 周りは攻撃者・研究者双方の注目領域になっている。
- 同時期に Check Point Remote Access VPN の認証バイパス CVE-2026-50751（CVSS 9.3）がランサムウェアに悪用されており、CISA は KEV カタログに 3 件を追加。ネットワーク境界製品への攻撃集中が続く。

### なぜ過去最大規模になったのか

修正件数の増加は、(1) AI 支援による脆弱性発見の効率化で報告数自体が増えていること、(2) クラウド・AI 関連コンポーネントの追加で攻撃面が拡大していること、が背景として指摘されている。単発の異常値ではなく、今後も大規模な月例更新が常態化する可能性がある。

## 今後の注目点

- CVE-2026-45657（ワーム化可能な TCP/IP RCE）の PoC 公開・実攻撃の有無。公開されれば 2017 年の EternalBlue 級のインパクトになり得る
- 「RoguePlanet」への Microsoft の対応（定例外パッチの可能性）
- Check Point VPN への攻撃キャンペーンの拡大と、国内企業の境界機器パッチ適用状況
- 月例 200 件規模が常態化した場合の、企業のパッチ運用（検証→展開サイクル）への構造的影響
