# Pentagon AI 8社契約と Anthropic 排除の意味

- **日付**: 2026-05-06
- **カテゴリ**: Tech
- **ソース**: [CNN Business](https://www.cnn.com/2026/05/01/tech/pentagon-ai-anthropic) / [gHacks](https://www.ghacks.net/2026/05/04/pentagon-sign-ai-deals-with-openai-google-microsoft-nvidia-and-others-cutting-out-anthropic/) / [The Intercept](https://theintercept.com/2026/05/01/elon-musk-openai-lawsuit-trial/) / [Techmeme](https://www.techmeme.com/)

## 概要

国防総省（DoD）は OpenAI / Google / Microsoft / Amazon / Oracle / Nvidia / SpaceX / Reflection AI の 8 社と、機密ネットワーク（IL5 / IL6 相当）での AI 利用を含む包括契約を締結した。一方で、当初候補に挙がっていた Anthropic は契約から外された。表向きの理由は「サプライチェーン上のリスク」だが、実態は「Claude を全ての合法目的（自律兵器・大量監視を含む）に使う」条項を Anthropic が拒否したことにある。

トランプ政権はこの拒否を受けて Anthropic との関係断絶を表明したが、カリフォルニア連邦地裁は政府が Anthropic との既存契約を一方的に破棄する動きを差し止めている。並行して、米 Center for AI Standards and Innovation は Google DeepMind / xAI / Microsoft の未公開モデルにも事前リスク評価のためアクセスする枠組みを拡大し、OpenAI / Anthropic を巻き込んだ自主協力体制を更に広げた。

## 詳細

### 契約スコープと運用範囲

- **対象環境**: 機密ネットワーク（NIPR/SIPR/JWICS 相当）での AI 推論・分析・大規模データ処理・物流。
- **想定ワークロード**: 国防情報の要約、衛星画像解析、サイバー作戦支援、後方支援最適化、武器システムへの周辺機能（標的識別の支援等）。
- **直接の自律兵器利用** は明文では禁止されていないものの、ガードレールは個別契約・運用 SOP に依存する形になる。

### Anthropic 除外の構図

- Anthropic は責任ある利用ポリシー（AUP）で「自律兵器」「大量監視」を一律禁止と明記しており、DoD の包括ライセンスとは整合しない。
- 商業面では、同社は Blackstone / Hellman & Friedman / Goldman Sachs と合計 $1.5B 規模の合弁を発表し、エンタープライズ AI サービスへ舵を切った。Google からの最大 $40B 投資、AWS / Trainium との連携も継続。
- 結果として Anthropic は「DoD と組まない代わりに、金融・大企業向けで稼ぐ」明確なポジショニングを取った形に。

### Big Tech 各社の温度差

- **OpenAI / Microsoft / Oracle**: 既存政府事業の延長で抵抗が小さい。
- **Google**: 過去の Project Maven 騒動を経て、再び DeepMind 内部に強い反発（UK 拠点で組合化投票）。
- **Amazon / Nvidia**: クラウド・GPU 供給という形で自然に組み込まれる構造。
- **SpaceX / Reflection AI**: 新興勢として「米国製 AI スタック」の象徴的存在。

### 法廷闘争と「AI と司法」のせめぎ合い

カリフォルニア連邦地裁が Anthropic との契約破棄を差し止めたことは、政権による恣意的な「契約解除」をチェックする重要な前例となる。今回の裁定は契約自由・独立行政原則の観点で広く議論を呼んでおり、AI ベンダーが「政府との取引で AUP を貫けるか」というガバナンス論点を一段高めた。

## 今後の注目点

- **米国版「AI ベンダー二分化」の固定化**: DoD 採用の Big Tech 8 社と、AUP を堅持して企業・金融セクターに振る Anthropic という二極化が進む。日本企業にとっては、どちらの軌道に乗る AI を業務インフラに採用するかが地政学的判断にも結びつく。
- **AUP・モデル使用条件の標準化議論**: 「合法目的すべて」型ライセンスを許容するかどうかが、各国政府調達ガイドラインで論点に。EU AI Act のハイリスク分類運用や、英国・日本の防衛 AI 調達でも追随的議論が起きる見込み。
- **DeepMind 組合化の波及**: 2026 年内の他 AI ラボへの組合運動拡大は、エンジニア採用市場と AI 倫理ガバナンスを同時に揺らす可能性。
- **裁判結果が AI ベンダー全体に与える影響**: 連邦政府が AUP 違反を理由に契約を一方的に切れない、という前例は他のベンダーにも波及。OpenAI / Google などが将来的に同様の AUP を強化する余地が生まれる。
- **「自律兵器ガードレール」の技術的実装**: モデル側でのポリシー強制、Constitutional AI 様のメカニズムを「契約の必須条件」として標準化する動きの萌芽。
