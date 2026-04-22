# Google Cloud Next 26: 第8世代 TPU と Gemini Enterprise が示す「コントロールプレーン」戦略

- **日付**: 2026-04-23
- **カテゴリ**: Tech
- **ソース**:
  - [Sundar Pichai shares news from Google Cloud Next 2026 — Google Blog](https://blog.google/innovation-and-ai/infrastructure-and-cloud/google-cloud/cloud-next-2026-sundar-pichai/)
  - [Our eighth generation TPUs: two chips for the agentic era — Google Blog](https://blog.google/innovation-and-ai/infrastructure-and-cloud/google-cloud/eighth-generation-tpu-agentic-era/)
  - [TPU 8t and TPU 8i technical deep dive — Google Cloud Blog](https://cloud.google.com/blog/products/compute/tpu-8t-and-tpu-8i-technical-deep-dive)
  - [Google splits TPU 8 to chase Nvidia on inference cost — implicator.ai](https://www.implicator.ai/google-splits-tpu-8-into-training-and-inference-chips-to-chase-nvidia/)
  - [Google Cloud Next 2026 preview: The real story isn't AI — it's the control plane — SiliconANGLE](https://siliconangle.com/2026/04/20/google-cloud-next-2026-preview-real-story-isnt-ai-control-plane/)

## 概要

Google は 4/22 から開幕した Google Cloud Next 26 で、第8世代 TPU を「学習向け TPU 8t」と「推論向け TPU 8i」の 2 製品に分割し、それぞれに最適化したネットワークトポロジを発表した。同時に Gemini Enterprise Agent Platform、120,000 社のパートナーを巻き込む $750M ファンド、Gemini 3.1 Pro / Flash Image / Veo 3.1 Lite / Lyria 3 Pro を一気に公開。表面上は「AI モデルとチップの強化」だが、業界アナリストの一致した見立てでは、本当の主題はエージェントを統治する「コントロールプレーン」の獲得競争である。

## 詳細

### TPU 8t と TPU 8i の役割分担

これまで一系統だった TPU シリーズを、第 8 世代では明確に「学習」と「推論」で別アーキテクチャに切り出した。

- **TPU 8t（training）**: 1 ポッドあたり最大 9,600 チップ。実績ある **3D torus** トポロジを採用し、massive な事前学習・継続学習を一括で抱えるワークロード向け。世代比で per-pod 性能 3x。
- **TPU 8i（inference）**: 1 ポッドあたり最大 1,152 チップ。新設計の **Boardfly** インターコネクトを採用し、4 チップのリング × 8 ボードのフルメッシュ × 36 グループという階層構成。OCS（Optical Circuit Switch）でグループ間を接続し、最大 7 ホップで全チップ間通信が完結。1024 チップ構成では 3D torus 比でホップ数を 56% 削減し、all-to-all 遅延を最大 50% 改善する。

学習はバッチでスループット重視、推論は低遅延・高並列が重要──というワークロードの性質差を、ネットワークトポロジレベルで分離した格好。Nvidia Rubin と Axion CPU を統合した「AI Hypercomputer」のコンセプトに乗せて、エージェント時代に必要な「持続的・対話的・並列」な推論キャパを TPU 8i 側で稼ぐ意図が明白だ。

### Gemini Enterprise Agent Platform

Gemini Enterprise は単なる「Gemini を企業に売る」プラットフォームではなく、エージェントを 1) 設計し 2) 配布し 3) 運用監視する一連のライフサイクルを覆うレイヤーへ進化した。新機能のうち重要なのは:

- **Agent Designer**: スケジュール／トリガーベースの sophisticated エージェントを GUI で設計
- **Long-running agents**: 複数日にまたがるビジネスプロセスを継続実行
- **Inbox**: 各エージェントが上げてきたアクション・確認事項を統合管理
- **Skills**: 反復タスクをショートカット化して再利用

加えて、第三者エージェント（OpenAI Codex / Claude Code 等）を企業ポリシーに従って取り込むためのガバナンス層を整備した。MCP の Linux Foundation 移管が直近で進んだことともあわせ、「マルチエージェント・マルチベンダー前提でも企業が制御できる場所」を Google Cloud に確保しに来ている。

### $750M パートナーファンドと「control plane」論

SiliconANGLE が事前の preview 記事で指摘していたとおり、本イベントの真のメッセージは「AI 性能競争」ではなく「誰がエージェントの control plane を握るか」である。$750M のパートナーファンドは、120,000 社のシステムインテグレータ／ISV を Gemini Enterprise の周辺に囲い込み、Salesforce の Headless 360（同じ週に発表）とのパッケージ販売を加速させるための弾薬とみてよい。

## 今後の注目点

- TPU 8i の対 Nvidia 推論コスト比優位性（GPU 比トークン単価）が公開されるか。Google は明示的な数値を出していないが、ベンチマーク再現が出始める 5 月以降の評価が焦点。
- Boardfly トポロジが OCP（Open Compute Project）に開示されるかどうか。Hyperscaler 各社のネットワーク設計の標準化動向に影響する。
- Gemini Enterprise の Inbox / Skills が実運用でエージェント疲れ（agent fatigue）を緩和できるか。Salesforce Agentforce、Microsoft Copilot Studio との UX 比較。
- AAIF（Agentic AI Foundation）配下に移った MCP との互換性をどこまで深めるか。Google が独自プロトコルに寄せれば「control plane」戦略は強化されるが、エコシステム分断のリスクも。
