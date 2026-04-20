# Claude Opus 4.7 の公開とフロンティアモデル競争の現在地

- **日付**: 2026-04-21
- **カテゴリ**: Tech
- **ソース**: [Anthropic — Introducing Claude Opus 4.7](https://www.anthropic.com/news/claude-opus-4-7) / [VentureBeat](https://venturebeat.com/technology/anthropic-releases-claude-opus-4-7-narrowly-retaking-lead-for-most-powerful-generally-available-llm) / [Vellum AI](https://www.vellum.ai/blog/claude-opus-4-7-benchmarks-explained)

## 概要

Anthropic は 2026-04-16 に Claude Opus 4.7 を一般提供した。エージェント系コーディング、ツール利用、コンピュータ操作、金融分析の主要ベンチマークで GPT-5.4 と Gemini 3.1 Pro を上回り、「商用で利用可能な最強モデル」の座を小差で取り戻した位置付け。API 価格は Opus 4.6 と同じ $5/$25 per MTok に据え置かれており、性能向上分を価格改定せずに吸収しているのが特徴。

OpenAI / Anthropic / Google の 3 社が 4 月頭に Frontier Model Forum 経由で中国勢の adversarial distillation に共闘を表明した文脈に直結する動きでもあり、フロンティア競争は「性能差」から「運用統制と配布網」の競争に移りつつある。

## 詳細

### ベンチマーク・性能

| 指標 | Opus 4.7 | 比較 |
|------|----------|------|
| SWE-bench Pro | 64.3% | Opus 4.6 の 53.4% から +10.9pt |
| GPQA Diamond | 94.2% | 先端モデルと互角 |
| 視覚推論（with tools） | 91.0% | Opus 4.6 の 84.7% から +6.3pt |
| Knowledge Work Elo | 1,753 | GPT-5.4 は 1,674、Gemini 3.1 Pro は 1,314 |

直接比較可能な全 11 ベンチマークのうち Opus 4.7 が GPT-5.4 を上回ったのは 7 勝 4 敗で、差は着実に縮まっている。Anthropic 自身も未公開の内部モデル「Mythos」は上回れていないと認めている。

### 新規 API 制御

- **`xhigh` effort レベル**: 推論品質と応答速度のトレードオフを調整する最上位オプション。
- **タスクバジェット**: 開発者がトークン消費を明示的に制限可能。
- **`/ultrareview` コマンド**: コード変更に対する厳密レビューを行うモード。エージェント用途での誤作動抑制を狙う。

### ビジョン強化

画像入力の長辺を最大 2,576 ピクセル（約 3.75 MP）までサポート。従来比で 3 倍以上の解像度で、スライド・ダッシュボード・スクリーンショット主体のエージェントワークフローに効く。

### セキュリティ機能

サイバーセキュリティ領域の禁止・高リスク用途を自動検出してブロックする仕組みを強化。正当な脆弱性研究者向けに個別認証プログラムを用意し、防御用途の継続性を維持する設計。

## 今後の注目点

- **Mythos の公開タイミング**: Anthropic 内部で Opus 4.7 を上回るモデルが既に存在する点が公表されており、OpenAI の次期更新と競合する形で 2026 Q3–Q4 の投入が予想される。
- **運用統制がフロンティア差別化要因に**: `xhigh` / バジェット / `/ultrareview` のように「失敗を減らす」方向の API 制御が増えている。エージェント運用の信頼性を SLA 化できるかが次の勝負。
- **distillation 対策の持続可能性**: Frontier Model Forum の intelligence sharing が中国勢のキャッチアップをどこまで遅らせるか。Anthropic が単独で 1,600 万件の不正リクエストを観測している規模感を踏まえると、モデル提供経路の署名・監査が業界標準化する可能性が高い。
- **価格の硬直化**: Opus 4.6 と同価格で 4.7 を投入したことで、Anthropic の単価は「性能で値上げする」戦略から「性能で利用量を引き上げて粗利を維持する」戦略に寄っている。IPO 観測と合わせ、収益モデルの説明性が問われる局面に入った。
