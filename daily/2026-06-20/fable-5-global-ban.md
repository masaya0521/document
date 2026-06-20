# Fable 5 グローバル禁止の経緯と論点

- **日付**: 2026-06-20
- **カテゴリ**: Tech
- **ソース**: [Anthropic 公式声明](https://www.anthropic.com/news/fable-mythos-access) / [Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/trump-adviser-david-sacks-says-anthropic-refused-to-fix-fable-5-jailbreak-before-us-export-controls) / [explainx.ai](https://www.explainx.ai/blog/us-government-bans-fable-5-mythos-5-anthropic-export-control-2026)

## 概要

2026年6月、米政府の指示により Anthropic のフロンティアモデル「Fable 5」および「Mythos 5」へのアクセスが停止された。発端は、米ホワイトハウスが Fable 5 の jailbreak（安全制御の回避）と、それを通じた中国系グループによるアクセスの可能性を安全保障リスクと判断したことにある。ホワイトハウスの AI 担当顧問 David Sacks は、政府が当初 Anthropic の CEO Dario Amodei に「jailbreak を修正するか、モデルをオフラインにするか」の二択を提示したが、Amodei が両方を拒否したと公表した。事態は当初の限定的なアクセス剥奪から、グローバルなモデル禁止へと段階的にエスカレートした。

## 詳細

### 発端：SK Telecom と中国接触懸念

SK Telecom は、Anthropic の第2波となる約150のパートナー組織に加わり、Project Glasswing を通じて Mythos への早期アクセスを確保していた。しかし親会社 SK Group が2009年まで China Unicom の株式を保有していた歴史的な対中ビジネス関係が問題視された。米政府は Anthropic に SK Telecom のアクセス剥奪を命じ、同社は即座に応じた。報道によれば、Anthropic はホワイトハウスが中国によるアクセスを懸念する中、わずか90分でアクセス制限を求められたという。

### jailbreak の深刻度を巡る評価の対立

Anthropic は問題の回避手法を検証し、「既知かつ軽微な脆弱性が少数表面化したに過ぎず、OpenAI の GPT-5.5 を含む他の公開モデルでも同様に発見可能」と説明し、深刻ではないとの立場を取った。一方で米政府はフロンティアモデルの jailbreak の完全排除を要求。セキュリティ専門家は「フロンティアモデルで jailbreak を完全にゼロにすることは技術的に不可能」と指摘しており、要求自体の現実性が論点となった。

### エスカレーションと復旧の動き

- David Sacks は禁止前に「修正 or de-deploy」の最後通牒を提示したと明かし、Amodei はいずれも拒否。
- 6/18 時点（禁止6日目）、Anthropic は第3のアジア太平洋拠点となるソウルオフィスを開設。Managing Director の Chris Ciauri は「数日以内」のモデル復帰可能性に言及。
- NAVER・Samsung SDS・LG CNS・Nexon・Hanwha 等の韓国大手が Claude の大規模導入を発表し、韓国市場へのコミットを強調。
- Anthropic と韓国科学技術情報通信部は、韓国語モデルの安全性評価とサイバー脅威情報共有に関する MOU を締結。
- 中国の MiniMax は open-weights のフロンティアモデル「M3」を「禁止に強い代替」として宣伝し、クローズドウェイトの Fable 5 との対比を打ち出した。

### 運用上の期限

利用者向けには、6/20 の返金締切、6/22 の無料トライアル終了という時間的制約が設定され、サブスクライバーへの対応が急がれた。

## 今後の注目点

- Fable 5 / Mythos 5 の実際の復旧タイミングと、その際に課される安全要件の内容。
- 「jailbreak ゼロ」要求が今後の AI 輸出規制の事実上の基準になるか否か。
- クローズドウェイト vs open-weights の安全保障論争で、MiniMax 等の中国製 open モデルがシェアを伸ばすか。
- 韓国を起点とした Anthropic のアジア展開と、米政府の対中懸念との緊張関係の行方。
