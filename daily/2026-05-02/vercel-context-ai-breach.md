# Vercel × Context.ai サプライチェーン侵害の全容

- **日付**: 2026-05-02
- **カテゴリ**: Tech
- **ソース**: [Vercel KB](https://vercel.com/kb/bulletin/vercel-april-2026-security-incident) / [The Hacker News](https://thehackernews.com/2026/04/vercel-breach-tied-to-context-ai-hack.html) / [TechCrunch](https://techcrunch.com/2026/04/20/app-host-vercel-confirms-security-incident-says-customer-data-was-stolen-via-breach-at-context-ai/) / [Trend Micro](https://www.trendmicro.com/en_us/research/26/d/vercel-breach-oauth-supply-chain.html)

## 概要

フロントエンド向けデプロイプラットフォーム Vercel は、4 月 19 日にサードパーティ AI ツール **Context.ai** 経由で侵害されたことを公表した。攻撃者は 2 月時点で Context.ai 側の従業員端末を Lumma Stealer で感染させ、Google Workspace の OAuth トークンを奪取。これを足がかりに Vercel 従業員の Google アカウントを乗っ取り、Vercel の本番環境にピボットして「非機密」とラベル付けされた環境変数を列挙・復号した。npm パッケージへの混入は確認されていないが、SaaS の OAuth 連携を起点にしたサプライチェーン攻撃の典型例として、開発者プラットフォーム業界に衝撃を与えている。

## 詳細

### 攻撃チェーン

1. **2026 年 2 月頃**: Context.ai 従業員のローカル端末が Lumma Stealer に感染。ブラウザの保存セッションと OAuth トークンが窃取される。
2. 攻撃者は Context.ai の Google Workspace OAuth トークンを利用し、Context.ai 内部のコラボレーション資産にアクセス。
3. その中から Vercel 従業員の個別 Google アカウントに紐づく権限を発見し、Vercel の Google Workspace 個人アカウントを乗っ取り。
4. 同アカウントから Vercel の管理コンソールに侵入し、API サーフェスの理解を活かして「非機密」と分類された環境変数を列挙・復号。
5. **4 月 19 日**: Vercel が異常を検知。CEO Guillermo Rauch が同日夜に X（旧 Twitter）で攻撃チェーンと Context.ai の関与を明示し、影響顧客への通知を開始。

### 影響範囲

- **流出**: 一部顧客の「非機密」環境変数（プレーンテキストに復号可能な値）。Vercel は該当顧客を特定し、即時のクレデンシャルローテーションを推奨。
- **流出していないと確認**: Vercel が公開する npm パッケージは GitHub / Microsoft / npm / Socket と協調調査の上で改ざんなしと結論。SDK・ビルドの汚染は否定された。
- ハッカーは BreachForums で「アクセスキー、ソースコード、API キー、内部デプロイメント認証、DB データ」の販売を主張したが、Vercel はこれらの主張を完全には裏付けない（一部は誇張・別ソースの可能性）と説明。

### この事案の含意

- **OAuth ベースの SaaS サプライチェーンが新しい侵入経路**: 直接 Vercel を狙うのではなく、Vercel 従業員が「副業的に」使っていた AI ツール経由で侵入。Single-Sign-On / OAuth による「便利な連携」がそのまま攻撃面になる。
- **「非機密」ラベルの過信**: Vercel は流出したのは非機密 env 変数のみと強調するが、顧客側ではビジネスロジック上のキー・URL・フィーチャーフラグが入っていた可能性があり、影響評価は顧客自身がやり直す必要がある。
- **AI スタートアップ側のセキュリティ未成熟**: Context.ai のような若い AI 企業が、ハイパースケール顧客に対して「信頼の橋」になり得る。CISO 配置・SOC2/ISO27001 整備が「製品」として重要化。
- 同時期に発生した ADT のランサムウェア（ShinyHunters、1,300 万件流出）と合わせ、2026 年 4 月は **OAuth × ランサムウェア × ストレラー** の三重奏で「サプライチェーン経由のクレデンシャル収奪」が事業リスクに昇格した月になった。

## 今後の注目点

- Vercel と類似の構造を持つ Netlify、Cloudflare Pages、Render などへの波及調査
- Google Mandiant の事後解析公表 — 攻撃者の帰属（国家アクター/犯罪集団のいずれか）
- 影響顧客の二次被害 — 流出した env 変数を起点にした下流の侵害が顕在化するか
- OAuth スコープ最小化、Just-in-Time 権限付与、SaaS 連携の継続的な棚卸しといった**OAuth ハイジーン**実装の業界標準化
- Lumma Stealer 系インフォスティーラーの撲滅オペレーション（米欧捜査機関が 2025 年から進めるテイクダウンの効果）
