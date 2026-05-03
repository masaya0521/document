# Pentagon が AI 契約から Anthropic を排除した意味

- **日付**: 2026-05-03
- **カテゴリ**: Tech
- **ソース**: [CNN Business](https://www.cnn.com/2026/05/01/tech/pentagon-ai-anthropic), [Military Times](https://www.militarytimes.com/news/pentagon-congress/2026/05/01/pentagon-freezes-out-anthropic-as-it-signs-deals-with-ai-rivals/), [The Hill](https://thehill.com/policy/technology/5858995-pentagon-ai-companies-classified-work-deal/)

## 概要

米国防総省は 2026年5月1日、機密ネットワーク上での AI 利用に関する契約を SpaceX、OpenAI、Google、Microsoft、Nvidia、AWS、Reflection の 7 社（一部報道では 8 社）と締結した。一方で、Claude を提供する Anthropic は契約から除外されており、Trump 政権は同社が Pentagon 向け利用に対して安全ガードレール（軍事用途で殺傷判断に AI を関与させない等）を要件として求め続けたことを「ブラックリスト入り」の理由に挙げている。

これは「Big Tech と政府の AI 統合がトップギアに入ったこと」と、「Trump 政権が AI 安全性を理由に商業的アクセスを制限し始めたこと」の双方を象徴する事案である。

## 詳細

### 経緯

- 2025〜2026 年初頭にかけて、Pentagon は Joint AI 戦略の一環で複数の商用 LLM を機密 (SIPR/JWICS) ネットワークで活用する枠組みを進めていた。
- Anthropic は当初から「致死性意思決定への関与禁止」「公開可能な safety case」など独自の利用条件を提示。Trump 政権はこれを「実戦運用を阻害する制約」とみなし、契約交渉から段階的に除外したと報じられている。
- 2026年4月29日の Big Tech 決算では Microsoft / AWS / Google Cloud の政府向け契約パイプラインが急拡大していることが明らかになり、5月1日の発表はそれを裏付ける形となった。

### 契約に含まれる企業の特徴

- **OpenAI**：GPT-5.4 系列を国防専用テナントで提供。
- **Google**：Gemini 3.x 系列＋ Vertex AI Government を統合。
- **Microsoft**：Azure Government 上の Copilot/Foundry スタック。
- **Nvidia**：機密ネットワーク用 Rubin 系 GPU クラスタ。
- **AWS**：GovCloud + Bedrock で他社モデルを再販。
- **SpaceX**：Starlink Defense + 衛星 ISR データ向け Inference。
- **Reflection**：オープンウェイト系米国 AI ラボ（新興プレイヤー）。

### Anthropic 側の立場

- Anthropic は Pentagon 向けにも Claude Gov を提供してきたが、利用規約として「殺傷判断や標的決定への直接利用を禁止」と明記。
- Pentagon 側はこれを「作戦上のフレキシビリティを損ねる」として評価せず、調達ベンダーから除外した。
- 一方で Anthropic は同時期に Google から最大 $40B の投資、AWS から $25B 超の投資を受けており、商業面では引き続き拡大基調。

## 含意

### 1. 政府市場での AI safety スタンスがコストになる構造

Anthropic は商業領域では「safety-first」を差別化要素にしてきたが、政府市場ではそれがマイナスに作用する局面が出てきた。今後、商業/政府で利用規約を分離するかどうかが、AI ラボ各社の戦略上の論点となる。

### 2. 公的調達の「AI ラボ × インフラ」垂直統合

OpenAI（Microsoft Azure 経由）、Anthropic（AWS / Google Cloud 経由）など、AI ラボはハイパースケーラー経由で政府にアクセスしてきた。今回 SpaceX や Reflection といった非ハイパースケーラー系も並列に契約されたことで、「ハイパースケーラーの再販モデル」だけが正解ではなくなった。

### 3. 規制の温度差

EU AI Act が 2026-08-02 に高リスクシステムの本格適用を迎える一方で、米国は連邦レベルの統一 AI 規制よりも調達権を通じた政策誘導に軸足を置きつつある。AI 規制の国際的なフラグメント化が一段進む。

## 今後の注目点

- Anthropic が「政府向け SKU」として安全制約を緩めた商品を出すか、あるいは民間 + 同盟国政府に絞る戦略を継続するか
- Reflection が機密ネットワーク向けで実装能力を示せるか（オープンウェイト系の信頼性検証）
- DoD 内での実運用フィードバック（殺傷判断への AI 関与の有無）と Congressional 監督の温度感
- 同様の「safety スタンスによる排除」が NSA / 諜報コミュニティ / 同盟国軍に波及するか
- EU AI Act 適用後、Anthropic が EU 市場で逆に有利なポジションを得る可能性
