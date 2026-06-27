# カスタム AI シリコンへのシフト

- **日付**: 2026-06-28
- **カテゴリ**: Tech
- **ソース**: [Tom's Hardware](https://www.tomshardware.com/tech-industry/semiconductors/custom-ai-asics-examined-from-broadcom-to-mtia), [Tech Times](https://www.techtimes.com/articles/317225/20260526/custom-ai-chips-outpace-nvidia-gpu-growth-2026-asic-shipments-set-triple-gpu-rate.htm), [Tech Startups](https://techstartups.com/2026/06/26/top-tech-news-today-june-26-2026/)

## 概要

2026年、AI ハードウェアの勢力図が NVIDIA GPU 一強からカスタム ASIC へとシフトしつつある。TrendForce 予測ではクラウド事業者のカスタム ASIC 出荷が2026年に44.6%成長と、GPU の16.1%を大きく上回る。OpenAI が Broadcom と共同で初の自社推論チップ「Jalapeño」を発表したことは、この潮流を象徴する出来事だ。Google・Apple・SpaceX に続き、主要 AI プレイヤーが単一サプライヤ依存からの脱却と TCO 削減を目指して自社シリコンへ動いている。

## 詳細

### なぜカスタム ASIC か

推論を本番規模で運用する場合、カスタムシリコンは従来の GPU に対して最大65%の TCO（総保有コスト）優位があるとされる。汎用性を犠牲にして特定ワークロードに最適化することで、電力効率と単位コストを大幅に改善できる。AI 利用が「学習中心」から「推論中心（実運用）」へ移るにつれ、この優位性が経営判断を左右するようになった。

### 主要プレイヤーのカスタムチップ

- **OpenAI**: Broadcom と共同で推論チップ「Jalapeño」を発表。自社モデルを設計プロセスに活用し9ヶ月で開発したのが特徴。本番デプロイは2027年を視野。
- **Google**: TPU（Broadcom が co-design）
- **Meta**: MTIA アクセラレータ
- **Amazon**: Trainium 3
- **Microsoft**: Maia 200
- **Anthropic**: 2026年に1ギガワット規模の TPU、2027年に3ギガワットへ拡張

### Broadcom の支配的地位

Broadcom と Marvell でカスタム AI ASIC の co-design 市場の推定95%を握る。ハイパースケーラーのチップ仕様を製造可能なシリコンへ翻訳するエンジニアリングパートナーとしての役割が決定的。Broadcom の2026会計年度 Q1 の AI 半導体売上は84億ドルで前年比106%増と急伸している。

### NVIDIA への含意

ハイパースケーラーが内部 AI ワークロードの増分を自社 ASIC で賄うようになると、NVIDIA への依存度は構造的に低下する。ただし NVIDIA も TSMC と組み AI を半導体製造自体に統合するなど、エコシステムの上流・下流双方で攻勢をかけている。「GPU か ASIC か」の二者択一ではなく、用途別の棲み分けが進む構図。

## 今後の注目点

- Jalapeño の実機性能と2027年デプロイの実現性
- TSMC の CoWoS 先進パッケージング供給がボトルネックを解消できるか（需給ギャップは年末に約10%へ縮小見込み）
- カスタム ASIC シフトが NVIDIA の成長率・株価に与える中長期影響
- AI データセンター向けチップ売上が2028年に1.2兆ドル超へ（SIA-Deloitte 試算）という巨大市場の獲得競争
