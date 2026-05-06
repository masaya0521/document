# GPT-5.5 Instant のハルシネーション削減手法

- **日付**: 2026-05-07
- **カテゴリ**: Tech
- **ソース**: [TechCrunch](https://techcrunch.com/2026/05/05/openai-releases-gpt-5-5-instant-a-new-default-model-for-chatgpt/) / [The Decoder](https://the-decoder.com/chatgpt-update-rolls-out-gpt-5-5-instant-with-fewer-hallucinations-and-more-personalized-answers/) / [Implicator AI](https://www.implicator.ai/openai-swaps-chatgpt-default-to-gpt-5-5-instant-cuts-hallucinations-52-5/)

## 概要

OpenAI は 5/5、ChatGPT のデフォルトモデルを **GPT-5.5 Instant** に切り替えた。本体である GPT-5.5（4/23 公開）の Instant 派生で、応答速度を維持しつつ事実誤認の削減を最大の売りに据えた。OpenAI 自身の公式ブログでは "ハルシネーション率 52.5% 減 / 不正確な主張 37.3% 減" と謳う一方、Deployment Safety Hub の数字を読み解くと「全プロンプト均一に 52% 減」ではなく「ハイステークスなクエリに限った計測」であり、計測区間の前提が成果の解釈を大きく左右する。

ChatGPT は週次アクティブユーザーが推定 8 億人を超えるため、デフォルトモデルの差し替えは事実上「世界最大のクライアントベース更新」と等価である。技術的トリックよりも、評価設計と運用配備の意思決定こそが今回のニュース価値の中心にある。

## 詳細

### 公称値の内訳と母集団

OpenAI が掲げた数値は3層に分かれる。

- **52.5% 減**: 「事実誤認のあった会話」と過去にユーザーが報告したサンプル群を再評価し、同条件で生じた誤主張の頻度を比較。母集団は明示的に "high-stakes prompts" に限定される。
- **37.3% 減**: 上記より広い "ユーザーが factual error を tag したセッション" 全体に対する不正確主張の割合。
- **23% / 3%**: Deployment Safety Hub に掲載された claim-level / response-level の正味改善幅。これは tool-enabled な実 ChatGPT トラフィックを正規化したスライス。

つまり「最大 52.5%」と「実運用ベースで 23%」の差は、評価対象の選び方の差である。Wire Blog が指摘した通り、これは "context engineering の勝利" であって、モデル本体のパラメトリック知識の純改善ではない。

### 主要ベンチマーク

GPT-5.5 Instant は性能面でも前モデルから一段上がっている。

| ベンチマーク | 旧モデル | GPT-5.5 Instant |
|--------------|---------|------------------|
| AIME 2025 (数学) | 65.4 | **81.2** |
| MMMU-Pro (マルチモーダル) | 69.2 | **76.0** |
| CharXiv (科学チャート読解) | 75.0 | **81.6** |

一方、AA-Omniscience（百科辞典的多分野知識）では精度 57% で過去最高ながら **86% のハルシネーション率** が記録されており、「広く浅い知識を答えさせる」と依然として誤りやすい構造は残存する。精度 vs キャリブレーションのトレードオフは未解決。

### 削減手法の推定

OpenAI は技術詳細を公開していないが、外部の観測と System Card の断片からは次の組み合わせと考えられる。

1. **Tool-enabled 既定挙動**: Web 検索・コード実行・メモリ参照などのツール利用を Instant モードでもデフォルト ON にし、parametric knowledge への依存を意図的に減らす。
2. **Safe Completions 化**: 確信度の低い主張を出さず "I don't know" を許容する報酬モデル調整。これにより不正確主張は減るが、回答の網羅性は落ちうる。
3. **長文記憶（メモリ）の制度化**: 会話横断の persistent memory を活用し、ユーザー固有事実の取り違いを抑制。
4. **GPT-5.5 Pro の parallel test-time compute からのバックポート**: Pro 版で採用された複数経路推論の一部を、Instant でも軽量に適用している可能性。

### 運用面のインパクト

- **金融・医療・法務などのレビュー業務**: high-stakes 区間での誤主張が大きく減るなら、人間の確認コストを直接削減できる。Anthropic が同週に金融向け事前構成エージェント10種を出した文脈とぶつかる。
- **OSS / 非公式ドキュメント領域**: AA-Omniscience 結果を踏まえると、ニッチ知識のレファレンス用途では依然として裏取り必須。
- **エージェント連鎖**: ハルシネーション削減はマルチステップ推論の成功率を非線形に押し上げる（誤りが連鎖する確率が二乗で効くため）。Codex / Operator 系のタスク完了率改善の方が、単発質問より体感差が大きい可能性。

## 今後の注目点

- **第三者ベンチマーク**: Vectara HHEM、HaluBench、SimpleQA などの独立リーダーボードで再現できるか。OpenAI 公称と外部測定値の乖離幅。
- **AA-Omniscience の改善遅延**: 「精度は上がる、ハルシネーション率は下がらない」分布が続くなら、知識統合（RAG / 専門アダプタ）が依然必要という結論になる。
- **Anthropic / Google の追従**: Claude / Gemini のハルシネーション削減アップデートのタイミングと評価設計。「同条件比較」の枠組みが業界標準になるか。
- **エンタープライズ採用条件への影響**: ハルシネーション率 SLA を要求する大企業契約で、計測区間（"high-stakes only"）の定義が契約上の論点になる可能性。
- **GPT-5.5 Pro parallel compute の Instant 適用範囲拡大**: コスト・レイテンシのトレードオフをどこまで詰められるか。
