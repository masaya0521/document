# GPT-5.4・Claude Mythos 5・Gemini 3.1 Pro: 2026 春のフロンティアモデル比較

- **日付**: 2026-04-23
- **カテゴリ**: Tech
- **ソース**:
  - [Claude Mythos 5: The First 10-Trillion-Parameter Model — Medium / AI & Analytics Diaries](https://medium.com/ai-analytics-diaries/claude-mythos-5-the-first-10-trillion-parameter-model-scaling-laws-hit-a-new-milestone-fa542be336f8)
  - [Mythos Preview — red.anthropic.com](https://red.anthropic.com/2026/mythos-preview/)
  - [Anthropic's latest AI model is sparking fears from cybersecurity experts — CBC](https://www.cbc.ca/news/business/mythos-anthropic-ai-explainer-9.7171597)
  - [LLM News Today (April 2026) — llm-stats.com](https://llm-stats.com/ai-news)
  - [AI News Last 24 Hours: April 2026 — devFlokers](https://www.devflokers.com/blog/ai-news-last-24-hours-april-2026-model-releases-breakthroughs)
  - [Sundar Pichai shares news from Google Cloud Next 2026 — Google Blog](https://blog.google/innovation-and-ai/infrastructure-and-cloud/google-cloud/cloud-next-2026-sundar-pichai/)

## 概要

2026 年 4 月、3 大ラボ（Anthropic / OpenAI / Google）から同月内にフラッグシップモデルが揃って公開され、いわゆる「フロンティアモデル」のレイヤーが質的に塗り替わった。Anthropic は 10 兆パラメータの **Claude Mythos 5** を Project Glasswing として限定プレビュー、OpenAI は **GPT-5.4** が OSWorld-Verified で 75.0% を達成しデスクトップ自律操作を実用域へ、Google は Cloud Next 26 で **Gemini 3.1 Pro / Flash Image / Veo 3.1 Lite / Lyria 3 Pro** を一斉投入。スケール・自律性・マルチモーダルという 3 軸のいずれもアップデートが進み、開発者と企業導入の判断軸が再構成されつつある。

## 詳細

### Claude Mythos 5（Anthropic）

- **規模**: 公称 10 兆パラメータ。MoE（Mixture of Experts）で 1 トークンあたり active が概ね 800B〜1.2T 程度と独立推定されている。
- **発覚経緯**: 3/26 にセキュリティ研究者 Roy Paz が Anthropic CMS の公開ミスを発見、3,000 件超のドキュメント中にドラフト発表記事が含まれていた。Anthropic は数時間で封鎖し、その後「step change である」と公式に認めた。
- **ポジショニング**: Claude Opus の上位に置かれるエンタープライズ／サイバーセキュリティ専用モデル。red.anthropic.com の Mythos Preview によると、主要 OS とブラウザ全体について 0-day を検出し exploit まで自動生成可能。最古事例は OpenBSD の 27 年もの既パッチ済みバグまで遡って発見した。
- **公開状況**: 一般公開はされず、Project Glasswing として一部企業・研究機関のみアクセス。CBC は「銀行・サイバーセキュリティ業界に懸念」と報じている。

### GPT-5.4（OpenAI）

- **デスクトップ自律性**: OSWorld-Verified で 75.0%（人間水準を超過）。ファイルシステム操作・ブラウザ操作・ターミナル操作を最小限の人間介入で完結。
- **Codex Labs**: 4/21 ローンチ。Codex 週間アクティブ開発者は 4 月初の 3M から 2 週間で 4M 超に。エージェント前提の IDE 体験を本気でメイン化しに来た。
- **OpenAI の路線**: モデル単体の知能ベンチではなく、「成果物を出すエージェント」として企業 OSS ワークロードに踏み込んでいる。

### Gemini 3.1 Pro / Flash Image / Veo / Lyria（Google）

- **3.1 Pro**: 推論ベースの ハードベンチ（Humanity's Last Exam）で 50% 超を達成、Claude Opus 4.6 と並ぶトップクラス。
- **Flash Image (Nano Banana 2)**: 画像生成・編集の高速バリアント。エージェント連動利用を前提にした安価＆高速 SKU。
- **Veo 3.1 Lite / Lyria 3 Pro**: 動画と音楽。マルチモーダル前提のエージェント体験を Gemini Enterprise Agent Platform 上で完結させる戦略。
- **TPU 連動**: 第 8 世代 TPU 8i（推論専用、Boardfly トポロジ）で推論コストを下げに来ており、コスト効率での攻勢が次の論点。

### 比較の論点

| 観点 | Claude Mythos 5 | GPT-5.4 | Gemini 3.1 Pro |
|---|---|---|---|
| 公開度 | 限定プレビュー | API/製品 | API/Vertex |
| 強み | サイバーセキュリティ・複雑コーディング | デスクトップ自律操作 | マルチモーダル・コスト |
| 主要リスク | Misuse／公開時の流出懸念 | 自律実行の責任分界 | エージェント濫立 |
| 主戦場 | 高ステークス専門領域 | 開発者ワークフロー | 企業エージェント基盤 |

## 今後の注目点

- Claude Mythos 5 の一般公開／API 提供時期と価格設計（10T パラメータでの推論コストをどう正当化するか）。
- GPT-5.4 の OSWorld 75.0% が現場の生産性に転化するまでのリードタイム。「エージェントが PR を出すが人間レビューがボトルネック」状態の企業は多い。
- Gemini 3.1 Pro の Humanity's Last Exam スコアが 50% を超えた後、ベンチマーク自体の延命策（より厳しい後継評価）の登場。
- 3 ラボ間で「エージェントが他社モデルを呼び出す」相互運用性（MCP, AGENTS.md, Goose の AAIF ガバナンス）が安定運用に乗るか。
- 規制側（EU AI Act 高リスク用途、米国 NIST AI RMF）が Mythos 5 級モデルにどのような追加義務を課すか。
