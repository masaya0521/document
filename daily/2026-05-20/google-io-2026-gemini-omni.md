# Google I/O 2026 — Gemini Omni と Intelligent Eyewear が示すマルチモーダルの臨界点

- **日付**: 2026-05-20
- **カテゴリ**: Tech
- **ソース**:
  - [Google Blog — Google I/O 2026 Collection](https://blog.google/innovation-and-ai/technology/developers-tools/google-io-2026-collection/)
  - [9to5Google — Everything Google announced at I/O 2026](https://9to5google.com/2026/05/19/google-io-2026-news/)
  - [TechCrunch — With Gemini 3.5 Flash, Google bets its next AI wave on agents](https://techcrunch.com/2026/05/19/with-gemini-3-5-flash-google-bets-its-next-ai-wave-on-agents-not-chatbots/)
  - [VentureBeat — Gemini 3.5 Flash can slash enterprise AI costs](https://venturebeat.com/technology/google-says-gemini-3-5-flash-can-slash-enterprise-ai-costs-by-more-than-1-billion-a-year)

## 概要

5/19 開催の Google I/O 2026 で、Google は AI モデル群を「会話する Chatbot」から「行動する Agent」へとリポジショニングした。中心は新モデル 2 本 — **Gemini Omni**（あらゆる入力から映像までを生成するマルチモーダル基盤）と、**Gemini 3.5 Flash**（3.1 Pro をコーディング・エージェント系ベンチで上回り、4 倍の出力速度を実現するフラッシュ層）。さらに、AI に最適化された **Intelligent Eyewear** を秋に投入することを発表し、ハードウェア側でも勝負を仕掛けてきた。

## 詳細

### Gemini Omni — 「世界理解」の総合プラットフォーム

- 映像を起点に、任意の入力からあらゆる出力（映像・音声・テキスト・UI）を生成。
- マルチモーダル理解・編集能力の大幅な飛躍を Google は強調。
- AI 映像生成ツールとしての位置付けも明示され、Sora / Veo 系競合への直接対抗。

### Gemini 3.5 Flash — エージェント時代の標準モデル

ベンチマーク（vs Gemini 3.1 Pro）:

| ベンチ | 3.5 Flash | 3.1 Pro |
|--------|-----------|---------|
| Terminal-Bench 2.1 | **76.2%** | 下回る |
| MCP Atlas | **83.6%** | 下回る |
| CharXiv Reasoning | **84.2%** | 下回る |
| Humanity's Last Exam | 40.2% | **44.4%** |
| ARC-AGI-2 | 72.1% | **77.1%** |

**「実務 ≒ コーディング / エージェント」では 3.5 Flash が 3.1 Pro を超えた**点が最大の事件。一方、純粋な知識量 / 抽象推論では Pro に劣後する。Google は「実務用途は Flash で十分」というメッセージで、コストパフォーマンスの常識を一段塗り替えに来た。

- 価格: **$1.50 / $9 per 1M tokens**（input / output）
- コンテキスト: **1M トークン**
- 速度: 既存フロンティアモデルの **約 4 倍**（出力トークン秒）
- 提供: Gemini app, AI Studio, Antigravity, Gemini API, AI Mode (Google Search)

VentureBeat 記事によれば、Google は「企業のエンタープライズ AI コストを年間 $1B 以上削減できる」と試算を提示。これは事実上「Pro クラスを Flash 価格で」というポジショニング。

### エージェント機能群

- **Antigravity**: エージェント・ファーストの開発プラットフォーム。「書くツールから行動するエージェント」への移行を明示。
- **Gemini Spark**: Gmail, Docs, Workspace と統合され、夏には MCP 経由でサードパーティへ拡張。米国の AI Ultra ユーザーから順次解放。
- **Daily Brief**: Gmail / Calendar / Tasks を横断する一日のパーソナル・ダイジェスト。AI Plus / Pro / Ultra 層に米国で配信開始。
- **Universal Cart**: AI がショッピングカートを能動的にチェック・最適化。Search の体験設計を「AI が代理購入する」モデルへ移行。
- **Information agents in Search**: Search 体験の「30 年で最大級のアップグレード」と Google は表現。

### Intelligent Eyewear

- 秋発売予定の「AI に最適化されたメガネ」を I/O のステージで実演。
- Vision Pro / Meta Ray-Ban / Snap Spectacles と直接競合するレンジ。
- Gemini Omni のマルチモーダル能力を「身に着ける形」で展開する戦略の核と位置付けられた。

## 今後の注目点

- **Vertical / Enterprise への浸透**: $1.50/$9 価格設定は、企業向け推論コストを書き換えるレンジ。エンタープライズで Anthropic / OpenAI からの乗り換えが起こるかが最大の競争軸。
- **MCP 拡張のロードマップ**: Spark の MCP 経由 3rd-party 拡張が夏に予定通り進むかが、Google の「エージェント・エコシステム化」の試金石。
- **Antigravity の採用度**: GitHub Copilot, Cursor, Windsurf, Claude Code との直接競合。シェア争いはコーディング・エージェント市場の構造を左右する。
- **Intelligent Eyewear の実用性**: バッテリー、視野角、プライバシー、価格 — 4 つすべてで Meta Ray-Ban を超えられるかが秋商戦のポイント。
- **Gemini Omni の生成品質**: Sora 系・Veo 系との比較で「世界モデルとしての一貫性」が評価軸。
