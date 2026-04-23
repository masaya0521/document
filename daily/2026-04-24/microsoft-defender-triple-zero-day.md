# Microsoft Defender 3重0day と更新阻止型エクスプロイト

- **日付**: 2026-04-24
- **カテゴリ**: Tech
- **ソース**:
  - [The Hacker News](https://thehackernews.com/2026/04/three-microsoft-defender-zero-days.html)
  - [Picus Security](https://www.picussecurity.com/resource/blog/bluehammer-redsun-windows-defender-cve-2026-33825-zero-day-vulnerability-explained)
  - [SOCRadar](https://socradar.io/blog/bluehammer-redsun-undefend-windows-defender-0days/)
  - [BleepingComputer: CISA orders feds to patch BlueHammer](https://www.bleepingcomputer.com/news/security/cisa-orders-feds-to-patch-microsoft-defender-flaw-exploited-in-zero-day-attacks/)
  - [Help Net Security](https://www.helpnetsecurity.com/2026/04/17/microsoft-defender-zero-days-exploited/)

## 概要

2026 年 4 月、Windows Defender に対して BlueHammer（CVE-2026-33825）、RedSun、UnDefend の 3 つの 0day が立て続けに公開され、13 日間以内に全てが実環境で悪用され始めた。BlueHammer は 4 月の Patch Tuesday で修正されたが、RedSun と UnDefend は本記事執筆時点（4 月 24 日）で未パッチであり、特に UnDefend は「Defender 自身の定義更新を停止させて検知能力をサイレントに劣化させる」タイプで、一般的な EDR 運用前提を揺るがす性質を持つ。

## 詳細

### タイムライン

- **4 月 7 日**: BlueHammer（CVE-2026-33825）が PoC 付きで公開。
- **4 月 10 日**: BlueHammer の野良悪用が観測され始める。
- **4 月（Patch Tuesday）**: BlueHammer は修正パッチ配布、CISA は連邦機関に適用を命令（KEV 追加）。
- **4 月 16 日**: RedSun と UnDefend の悪用を観測。
- **4 月 17 日**: 研究者が RedSun / UnDefend を追加公開、3 件が同時期に実攻撃で使用されていると報じられる。

### BlueHammer（CVE-2026-33825, パッチ適用済み）

- ローカル権限昇格（LPE）。
- 原因は Windows Defender の脅威除去エンジンにおける TOCTOU レース条件。マルウェア削除時にパスが再検証されない瞬間をついて、特権的なファイル操作を任意のパスに向けられる。
- 完全パッチ済みの Windows 10 / 11 でも、非特権ユーザーが SYSTEM 権限を取得可能。
- 4 月 Patch Tuesday で修正済みだが、CISA がカタログに入れるほど実害が確認されている。

### RedSun（未パッチ）

- Defender のクラウドタグ付きファイルの取り扱いを悪用した権限昇格テクニック。
- 非特権ユーザーがシステムパスを上書き可能になり、BlueHammer と同様に SYSTEM 昇格に繋がる。
- 4 月 24 日時点で修正パッチが出ていない。

### UnDefend（未パッチ）

- Defender の定義ファイル更新機構を妨害する、新型の「保護そのものを削る」タイプ。
- 非特権ユーザーでも実行可能。
- 実行後、Defender が定義アップデートを受け取れなくなり、時間経過とともに新種マルウェアへの盲点が広がる。
- 可視的なサービス停止やアラートを伴わず、EDR の劣化がサイレントに進行する。

### なぜ構造的に厄介か

1. **Defender 自身が攻撃の起点**: LPE + 更新妨害が Defender のロジック内部に根を張っており、「EDR を信じて検知運用する」という前提にヒビが入る。
2. **連鎖型の運用劣化**: BlueHammer だけ塞いでも、RedSun + UnDefend の組合せで「SYSTEM 取得 → 定義更新停止 → 再侵入の隠蔽」というシナリオが成立する。
3. **PoC 流出後の拡散速度**: 4/7 公開 → 4/10 悪用 → 4/16 追加 0day 悪用、というサイクルが 2 週間以内に回っており、パッチウィンドウが極めて短い。
4. **組織横断的なリスク**: Windows Defender は MSP・エンタープライズでのデフォルト EDR として広く使われているため、影響面積が大きい。

## 今後の注目点

- **RedSun / UnDefend の追加パッチ**: 5 月 Patch Tuesday のタイミングで緊急対応（Out-of-Band も含む）があるか。
- **Defender 更新の健全性モニタリング**: 定義更新のタイムスタンプ・バージョン差分の可視化が「新たな最低限の運用要件」となる可能性。
- **検知回避前提の脅威モデル**: EDR 本体が劣化する攻撃に備え、独立した EDR / サードパーティログ基盤 / SIEM 側での異常更新停止検知が再評価されるはず。
- **サードパーティ EDR / 独立検知層**: Defender に一本化している組織は、検知補完層（独立フォレンジックエージェント、EDR テレメトリの外出し）を前倒しで検討する必要がある。
- **関連する AI セキュリティ動向**: 同月 OpenAI は防御特化の GPT-5.4-Cyber を発表しており、「大量の 0day に対応する SOC 運用を AI で補う」議論は今後さらに加速する見込み。
