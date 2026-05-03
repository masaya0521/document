# EU AI Act 2026-08-02 全面適用に向けた実務インパクト

- **日付**: 2026-05-03
- **カテゴリ**: Tech
- **ソース**: [European Commission](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai), [Pearl Cohen](https://www.pearlcohen.com/new-guidance-under-the-eu-ai-act-ahead-of-its-next-enforcement-date/), [Kennedys](https://www.kennedyslaw.com/en/thought-leadership/article/2026/the-eu-ai-act-implementation-timeline-understanding-the-next-deadline-for-compliance/)

## 概要

EU AI Act は 2026 年 8 月 2 日に主要部分（高リスク AI システムの実体的義務、Article 50 透明性、市場監視、罰則）が全面適用される。すでに 2025 年 2 月（禁止用途・AI リテラシー）と 2025 年 8 月（GPAI モデルのガバナンス）が段階的に発効しているが、実際に企業の実装/プロセスを大きく変えるのは今回の 2026 年 8 月マイルストーンである。

3 か月後に迫った時点で、欧州市場で AI 製品・サービスを提供する全企業（米国・日本含む域外事業者を含む）にとっては「対応の最終直線」となる。

## 詳細

### 主要な義務（2026-08-02 から発効）

1. **高リスク AI システムの実体要件**
   - リスク管理プロセス
   - データガバナンス（学習・検証・テストデータの品質）
   - 技術文書（Annex IV）と記録保持
   - 透明性・人間による監督
   - 精度・堅牢性・サイバーセキュリティ
   - 適合性評価（conformity assessment）と CE マーキング
   - 上市後の監視・インシデント報告

2. **デプロイヤー（利用側）の義務**
   - 利用文脈での指示書遵守
   - ログ保持
   - 基本権影響評価（特定領域）
   - 従業員への通知

3. **Article 50 透明性要件**
   - AI 生成コンテンツの機械可読なマーキング
   - チャットボットであることの開示
   - emotion recognition / biometric categorization の利用通知
   - ディープフェイクの開示

4. **罰則**
   - 高リスク違反：€15M または全世界売上 3% のいずれか大きい方
   - 禁止用途違反は €35M / 7%（2025 年 2 月から既に発効）
   - 不正確な情報提供：€7.5M / 1%

### 各国レベルで必要となる体制

- 各加盟国が **少なくとも 1 つの AI Regulatory Sandbox** を 8月までに設置義務
- 通知機関（notifying authorities）と市場監視機関（market surveillance authorities）の指定
- AI Office（欧州委員会内）が GPAI モデルを直接監督、加盟国当局と AI Board で調整

### 高リスクとされる主要ユースケース（Annex III）

- 重要インフラ（電力・水・交通）の安全部品
- 教育・採用・人事評価
- クレジットスコアリング、保険引受
- 公共サービス受給判定
- 法執行、移民、司法、民主的プロセス
- 生体認証、感情認識、生体カテゴライズ

### 実装上の典型的論点

- **GPAI 基盤モデル + 特定用途**：基盤モデル提供側（OpenAI/Anthropic 等）と、それを高リスクユースケースに組み込む企業の責任分界
- **OSS と研究開発の例外**：研究目的・自由研究の取り扱い、フリーかつオープンなライセンスの GPAI に対する義務軽減
- **書類整備工数**：技術文書・データガバナンス・利用ログのテンプレート化と運用負荷
- **域外適用**：EU 内ユーザーに影響する場合は米国・日本企業も対象。GDPR と同様の extraterritorial 構造

## 含意

### 1. AI 機能を持つ SaaS は ROI 検算が必要

採用、信用判定、HR 系、医療系、教育系の SaaS は実質的に Annex III に該当しがち。CE マーキング相当の運用コストを商品設計に織り込めるかが、欧州市場継続の判断材料となる。

### 2. OSS / オープンウェイトの恩恵と限界

オープンに公開された GPAI モデルは一定の義務軽減が認められるが、「systemic risk を有する」と判定されると免除は外れる。商業利用との接点で実務上は責任分界が複雑化する。

### 3. 米欧の規制温度差

米国は連邦統一 AI 法を持たず、調達権による政策誘導（Pentagon の Anthropic 排除など）に向かう一方、EU はルールベースで強制力のある法執行へ。グローバル AI 企業は「米国向け SKU」と「EU 向け SKU」を分ける必要が一段と強まる。

### 4. 日本企業への影響

日本のグローバル製造業（自動車・医療機器）と SaaS 企業は、欧州子会社・販売拠点経由で対象となる。AI ガバナンス体制（モデルカード、データシート、評価ログ、人間監督手順）の整備は実質的に必須。

## 今後の注目点

- 7月までに公表される予定の追加ガイダンス（特に technical documentation テンプレート、conformity assessment の具体的手順）
- 8月以降、最初に公開される執行事例（おそらく禁止用途関連の罰金の続報）
- GPAI Code of Practice の更新と、OpenAI / Anthropic / Google / Meta の対応状況
- 各国 Sandbox のスタートアップ受け入れ状況（Member State 間の競争）
- 米国の State 単位 AI 法（NY、California、Colorado 等）との二重コンプライアンス負担
- 日本の AI 推進法・ガイドラインとの整合と相互運用性
