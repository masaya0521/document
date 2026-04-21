# GPT-5.4 Thinking と OSWorld-Verified の人間超え

- **日付**: 2026-04-22
- **カテゴリ**: Tech
- **ソース**: [OpenAI: Introducing GPT-5.4](https://openai.com/index/introducing-gpt-5-4/) / [TechCrunch](https://techcrunch.com/2026/03/05/openai-launches-gpt-5-4-with-pro-and-thinking-versions/) / [DataCamp](https://www.datacamp.com/blog/gpt-5-4)

## 概要

OpenAI がリリースした GPT-5.4 シリーズのうち、推論強化版 "Thinking" が desktop 操作ベンチマーク「OSWorld-Verified」で 75.0% を達成した。人間の平均スコア 72.4% を初めて汎用モデルとして上回り、従来最高（Kimi K2.5 の 63.3%、Claude Sonnet 4.5 の 62.9%）に対しても 10pt 以上の大差を付けた。

computer use（画面を見てマウス・キーボードで操作するエージェント）領域は、直近数カ月で推論時間の "thinking" 増加と操作履歴の memory 活用が進み、スコアが急上昇している。GPT-5.4 Thinking はその到達点の 1 つであり、エージェントが実業務に耐える段階に入る節目と見られる。

## 詳細

### ベンチマークが測っているもの

OSWorld-Verified は、Ubuntu / Windows の仮想デスクトップ上で、LibreOffice・Chrome・Thunderbird・GIMP・VS Code 等を画面キャプチャ経由で操作しタスクを完遂するエージェント評価。キーボード・マウス操作とスクリーンショット認識の両方が要求され、従来のコード/数学ベンチマークと比べてノイズ耐性・長文計画・失敗からの復旧能力を正面から測る性質を持つ。

### GPT-5.4 Thinking の特徴

- **テストタイム計算の本格統合**: 推論時に深い試行を行うモードを標準搭載し、Agent ループの各ステップで内在的に reflection を挟む。
- **ツール呼び出しの効率化**: OpenAI によれば、GPT-5.4 は 15 ツール呼び出しで 75% に到達した一方、GPT-5.2 は約 50% 到達に 3 倍近いツール呼び出しを要した。単純な success rate 以上に「同じ成功を少ないコストで」という効率指標でも飛躍。
- **1M コンテキスト / Tool Search**: 長期タスクと大量ツールを扱う実運用を想定した設計。

### 周辺の意味合い

- エージェント系スタートアップ（Cursor 等のコーディング、RPA、QA 自動化）は基盤モデル依存度が高く、スコア 10pt 単位の更新は製品体験を左右する。
- 一方、human-verified と言えども、OSWorld の母集団は主に短〜中期の既知タスク。本番業務の曖昧タスクや長期タスクにはまだギャップがある。
- ベンチマーク飽和に伴い、Anthropic・Google・xAI の次モデルでは「OSWorld-Verified は超えて当然」の前提で、より長期・マルチエージェント連携評価への移行が進む見込み。

## 今後の注目点

- Anthropic Claude Mythos 5、Google Gemini 3.1 Pro の OSWorld-Verified / OSWorld-Long 追随スコア
- 企業導入時の computer use エージェントの SLA（失敗時 rollback、監査ログ）整備
- OSWorld-Verified の後継ベンチマーク（長期タスク、マルチモーダル統合）の登場
- エージェント運用コスト（ツール呼び出し回数 × 推論時間）の最適化競争
