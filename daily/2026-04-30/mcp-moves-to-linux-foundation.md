# Model Context Protocol が Linux Foundation 配下へ — エージェント標準のガバナンス転換

- **日付**: 2026-04-30
- **カテゴリ**: Tech
- **ソース**:
  - [Anthropic — Donating MCP and establishing AAIF](https://www.anthropic.com/news/donating-the-model-context-protocol-and-establishing-of-the-agentic-ai-foundation)
  - [Linux Foundation — Formation of AAIF](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation)
  - [The New Stack — Anthropic Donates MCP to AAIF](https://thenewstack.io/anthropic-donates-the-mcp-protocol-to-the-agentic-ai-foundation/)
  - [GitHub Blog — MCP joins the Linux Foundation](https://github.blog/open-source/maintainers/mcp-joins-the-linux-foundation-what-this-means-for-developers-building-the-next-era-of-ai-tools-and-agents/)
  - [InfoQ — OpenAI and Anthropic donate AGENTS.md and MCP](https://www.infoq.com/news/2025/12/agentic-ai-foundation/)
  - [Fazm — Open Source AI releases April 2026](https://fazm.ai/blog/open-source-ai-releases-april-2026)

## 概要

エージェント時代のデファクト標準と化していた Model Context Protocol (MCP) が、Linux Foundation 配下に新設された Agentic AI Foundation (AAIF) へ正式に寄贈・移管された。AAIF は Anthropic・Block・OpenAI が共同設立し、Google、Microsoft、AWS、Cloudflare、Bloomberg がサポーターとして参画。MCP は **Block の `goose`** および **OpenAI の `AGENTS.md`** とともに創設プロジェクトとして配置される。

「単一企業が定義する事実上の標準」から「複数ベンダー横断のオープンファウンデーション標準」への移行は、エージェント領域の合意形成プロセスを再定義する出来事である。MCP は 2025 年 11 月時点で月間 9,700 万 SDK ダウンロード、1 万を超えるアクティブサーバ、ChatGPT・Claude・Cursor・Gemini・Microsoft Copilot・VS Code 等が一級でサポートする規模に成長していた。

## 詳細

### なぜ今、寄贈するのか

Anthropic 自身は「プロトコルの将来をベンダー中立にすることが目的」と説明。MCP の利用範囲が同社プラットフォームに収まらず、競合他社の AI ランタイムに広く取り込まれた以上、独占的なガバナンスを維持することのほうが採用障壁になりつつあった。

OpenAI が同時に `AGENTS.md`（エージェント設計のドキュメント仕様）を寄贈した点も重要だ。これまで競合関係にあった 2 社が「下のレイヤ（プロトコル / ドキュメント仕様）はオープンにして、上のレイヤ（モデル品質・エージェント実装）で勝負する」という業界の暗黙合意を形にした格好。Linux Foundation を仲介することで、特定企業の交渉力に左右されない「IETF 的」な標準化ルートが整う。

### ガバナンスの実務

| レイヤ | 担当 | 内容 |
|---|---|---|
| AAIF Governing Board | Linux Foundation 配下 | 戦略投資、予算配分、メンバー獲得、新規プロジェクト承認 |
| MCP Maintainers | 既存メンテナ継続 | プロトコルの技術的方向性、SEP プロセス、リリース判断 |
| 商用ベンダー | Anthropic / OpenAI / Block / Google / MS / AWS 等 | 実装、フィードバック、エコシステム拡張 |

Anthropic 側のアナウンスは「MCP の日常運営は変わらない。意思決定者は変わらず、SEP プロセスで community input を取り込む形」と強調。これは Kubernetes が CNCF 入りした時に Google が中立化を強調したのと同型のメッセージだ。

### 「ベンダー中立」を担保する設計上の工夫

AAIF は Linux Foundation 内の Directed Fund として設けられ、独立した予算と意思決定機構を持つ。プロジェクト個別の技術的自治と、ファウンデーション全体の戦略的整合のバランスを取る構造で、CNCF や OpenSSF の運営パターンを踏襲している。

技術的には MCP 1.x の互換維持が前提で、SEP（Specification Enhancement Proposal）プロセスを通じてバージョンアップを管理する。直近のロードマップとして、エージェント間通信・権限境界・監査ログ・サンドボックスといった「マルチテナント運用のための拡張」が議論されている。

### エコシステムへの含意

- **開発者観点**: ライブラリ・SDK のメンテナンス継続が保証され、実装を MCP に賭けるリスクが低減。
- **エンタープライズ観点**: Linux Foundation の CLA や IP ポリシー下に置かれることで、社内導入のレビュー（特許・ライセンス）が容易になる。
- **競合プロトコル**: Google の A2A、LangChain の LangGraph などが共存。MCP は「ホストと外部ツール / リソースの接続規約」、A2A は「エージェント間の意思疎通」と棲み分けが進む見通し。
- **規制・標準化**: EU AI Act の透明性要求、米国 NIST のガイドラインなど、トレーサビリティ要件と接続するための土台になり得る。

### リスクと未解決の論点

1. **大手企業の影響力集中**: AAIF Governing Board に Anthropic・OpenAI・Microsoft・Google・AWS が並ぶ構造は、結局「主要 AI 提供者の協調体」になる懸念。中小プロバイダや学術界の声をどう反映するか。
2. **互換性の劣化リスク**: 異なる実装が「拡張」を独自に追加し、MCP の互換性が断片化する古典的問題。SEP プロセスの実効性が試される。
3. **セキュリティ標準の不在**: 「外部ツール接続」という性質上、認可・サンドボックス・サプライチェーン保証のベースラインが必要。CISA / OpenSSF との連携が今後の論点。
4. **OpenAI の本気度**: AGENTS.md は寄贈したが、ChatGPT 内のエージェント実装は引き続き OpenAI 独自仕様を併用している。MCP に完全に乗るかは未確定。

## 今後の注目点

- **AAIF の最初の理事会と運営規則公開**: 投票権、メンバーシップ階層、基金の運用方針。
- **MCP 2.0 ロードマップ**: 認可フロー、複数エージェント協調、トランザクション境界の仕様化。
- **競合プロトコルとの相互運用**: A2A / OpenAI Agent SDK との bridge 仕様。
- **エンタープライズ採用ケース**: Microsoft Copilot Studio、Salesforce Agentforce、ServiceNow が MCP に正式準拠するか。
- **セキュリティ研究**: MCP サーバ実装を狙う攻撃 (LiteLLM CVE-2026-42208 と類似) が増加するなか、参照実装の安全性監査がどう進むか。
- **規制との接続**: EU AI Act の高リスク AI システム要件、NIST AI RMF 上での MCP 位置付け。
