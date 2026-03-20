# NVIDIA GTC 2026 — Vera Rubinとエージェント時代の幕開け

- **日付**: 2026-03-21
- **カテゴリ**: Tech
- **ソース**: [NVIDIA Blog](https://blogs.nvidia.com/blog/gtc-2026-news/), [CNBC](https://www.cnbc.com/2026/03/16/nvidia-gtc-2026-ceo-jensen-huang-keynote-blackwell-vera-rubin.html), [StorageReview](https://www.storagereview.com/news/nvidia-gtc-2026-rubin-gpus-groq-lpus-vera-cpus-and-what-nvidia-is-building-for-trillion-parameter-inference)

## 概要

2026年3月16-19日にサンノゼで開催されたNVIDIA GTC 2026で、Jensen Huang CEOは次世代AIプラットフォーム「Vera Rubin」を中心に、7種類の新チップ、5種類のラック、そしてエージェントAI向けの包括的なソフトウェアスタックを発表した。BlackwellからVera Rubinまでの受注は2027年までに1兆ドルに達する見通しで、従来の5,000億ドルの予測を大きく上回った。

## 詳細

### Vera Rubinプラットフォーム

Vera Rubinプラットフォームは従来のコンピューティングをラックスケールの専用システムに分解するアーキテクチャを採用。主要コンポーネントは以下の通り。

- **Rubin GPU**: 次世代AIアクセラレータ。130万個のコンポーネントで構成され、前世代Grace Blackwell比でワット当たり10倍の性能を実現
- **Vera CPU**: エージェントAIに必要な逐次推論処理に最適化された新CPUアーキテクチャ
- **Groq 3 LPU**: 推論のデコードフェーズにおける決定的・低遅延トークン生成のための第3世代言語処理ユニット。256基のLPUを収容する専用ラックも発表

Azureが最初のハイパースケールクラウドプロバイダーとしてVera Rubin NVL72システムを稼働開始し、今後数ヶ月でグローバルに展開予定。

### 推論パイプラインの分離アーキテクチャ

NVIDIAの推論オーケストレーションソフトウェアは、推論パイプラインを分離する革新的なアプローチを採用している。

- **プリフィルとKVキャッシュ**: Vera Rubinに送信
- **フィードフォワードデコード**: Groq LPUに送信
- 両システムはEthernet上で特殊プロトコルを使い並列動作し、レイテンシを約半分に削減

結果として、GPU単体構成と比較して**トークン/ワットが35倍改善**され、高付加価値の45-150ドル/百万トークンの価格帯が解放された。

### Dynamo 1.0

AIファクトリー推論のための初の分散オペレーティングシステムとして「Dynamo 1.0」をオープンソースで公開。推論ワークロードの効率的なスケーリングを支援する。

### Agent Toolkit と NemoClaw

- **Agent Toolkit**: 自律型・自己進化型のエンタープライズAIエージェント構築のためのオープンソースモデル・ソフトウェア群。Adobe、Atlassian、Salesforce、SAP、ServiceNow等17社のソフトウェア大手がロードマップに統合を表明
- **OpenShell**: 安全性とセキュリティを確保した自己進化型エージェント構築のためのオープンソースランタイム
- **NemoClaw**: オープンソースのOpenClawプロジェクト上に構築された、常時稼働AIエージェントのセキュアなエンタープライズスタック。ワンコマンドインストール、プライバシーガードレール、OpenShellサンドボックスを備え、RTX PC、DGXシステム、クラウドインスタンスをエージェントホストに変換

### Physical AIとロボティクス

- 日産、BYD、Geely、いすゞ、現代がNVIDIA Drive Hyperionプログラムでレベル4自動運転車を開発
- **Alpamayo**: 自動運転車開発のためのオープンソースAIモデル群をGitHubとFoundryで公開
- **Cosmos**: 物理AI開発のためのワールドモデル

### パートナーシップ

- **Microsoft**: Microsoft FoundryとNVIDIAのオープンモデル・アクセラレーテッドコンピューティングを統合したエージェント・物理AIの統合プラットフォームを発表
- **Oracle**: GPU加速ベクトルインデックス構築でNVIDIAと協力。Oracle Private AI Services ContainerがNVIDIA GPUとcuVSオープンソースライブラリをサポート

## 今後の注目点

- Vera Rubinの実際の出荷時期と初期ユーザーからのパフォーマンスベンチマーク
- 推論パイプライン分離アーキテクチャが実運用でどの程度の効率改善を実現するか
- Agent Toolkitの採用拡大とエンタープライズAIエージェントのユースケース成熟度
- Groq LPUとの協業がNVIDIAのビジネスモデルに与える影響（従来の競合からパートナーへの転換）
- 1兆ドルの受注見通しが実際に達成可能かどうか
