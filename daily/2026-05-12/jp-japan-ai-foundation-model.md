# Japan AI Foundation Model — 1 兆パラメータ物理 AI 連合と国家戦略

- **日付**: 2026-05-12
- **カテゴリ**: Japan Tech
- **ソース**: [Japan Times](https://www.japantimes.co.jp/business/2026/04/12/companies/softbank-ai-new-firm/) / [SiliconANGLE](https://siliconangle.com/2026/04/13/japanese-tech-giants-launch-joint-venture-targeting-physical-ai-robots-machines/) / [Decrypt](https://decrypt.co/364241/japan-physical-ai-trillion-parameter-softbank-nec-honda-sony) / [TechCrunch](https://techcrunch.com/2026/04/05/japan-is-proving-experimental-physical-ai-is-ready-for-the-real-world/)

## 概要

SoftBank、NEC、Honda、Sony は 2026 年 4 月 12 日、「Japan AI Foundation Model Development（日本AI基盤モデル開発）」を共同設立した。1 兆パラメータ規模の物理 AI（physical AI）基盤モデルを構築し、ロボット制御・工場オペレーション・自律機械への実装を目指す国家規模の連合体だ。NEDO（新エネルギー・産業技術総合開発機構）が令和 8 年度（2026 年度）から 5 年間で約 1 兆円（約 63 億ドル）の AI 支援策を準備しており、新会社はこの資金プールへの第一申請者となる見通し。日本鉄鋼・神戸製鋼・三菱 UFJ・三井住友・みずほの主要金融機関も出資する。

訓練データ・モデル運用はすべて国内に留め、海外クラウド上では処理しない「データ主権」設計が特徴。経産省が 3 月に公表した「物理 AI で 2040 年に世界シェア 30% 獲得」目標とも符合する。

## 詳細

### 「物理 AI」というコンセプトの転換

従来の大規模言語モデル（LLM）が言語上の応答に閉じていたのに対し、物理 AI は「知覚 → 推論 → 物理世界での行動」までを一体で扱う。ロボットアーム、工場制御、自律走行車、ヒューマノイドが対象領域となる。米国では Nvidia、Figure AI、Tesla Optimus が物理 AI への投資を加速しており、中国も Unitree・Xpeng の Iron などで追随する。日本は SoftBank の計算インフラ、NEC のセキュリティ・行政 AI、Honda のロボティクスと自動運転、Sony のセンサー・エンタメ・実世界データという 4 軸を束ねる戦略を採る。

### 1 兆パラメータの意味

1 兆パラメータは現行フロンティアモデル（GPT-4o 系、Claude 4 系）と同等規模で、物理 AI 用途では「世界モデル」「動作生成」「マルチモーダル統合」を 1 モデルで処理する野心的な仕様。約 100 人の AI エンジニアを採用し、訓練インフラは AWS・GCP に依存しない国内 GPU クラスタを志向する（NEDO 支援の一部はクラスタ整備に充当される見通し）。

### データ主権というロジック

「digital deficit（デジタル赤字）」という日本の産業界の問題意識が背景にある。日本企業のオペレーショナルデータ（製造現場の感覚値、ライン制御ログ、医療データ等）は長年米国 AI パイプラインへ吸い上げられ、国内には対応プラットフォームが育たなかった。新連合はこのデータ流出を止め、国内で閉じたパイプラインを再構築する建付けだ。Anthropic と NEC が 2025 年末に発表した協業（AI ネイティブなエンジニアリングプラットフォーム）も、この文脈で再評価される。

### NEDO 1 兆円支援の構造

NEDO の支援策は以下のスキームで動く見込み:

1. **基盤モデル開発** — 新会社が主受託。世界モデル/物理 AI モデル開発
2. **計算インフラ整備** — 国内 GPU クラスタ・HBM 調達補助
3. **データ流通プラットフォーム** — 業界横断のデータシェアリング基盤
4. **アプリケーション実装支援** — 製造業・物流・医療・自動運転への実装プロジェクト

26 年度〜30 年度の 5 年計画で、米中の大型 AI 投資に対する「公的レバレッジ」として設計されている。

### 競合・連携の構図

| プレイヤー | 役割 |
|---|---|
| Japan AI Foundation Model（新連合） | 1 兆パラ物理 AI、国家旗艦 |
| Sakana AI | 生成 AI のフロンティア研究、独自アーキ |
| Hutzper、VRAIN Solution | 製造現場向け低遅延 Edge AI |
| Preferred Networks | 既存の物理 AI/ロボティクスプラットフォーマー |
| デジタル庁「源内」 | 行政 AI 基盤、国産 LLM 7 モデル試用 |

新連合は他プレイヤーを排除する設計ではなく、データ・モデル・実装プロジェクトのハブとして機能することが想定される。源内 OSS との接続レイヤや、Sakana AI とのモデル共同開発も中長期では選択肢となる。

## 今後の注目点

- 新会社の社名・組織体制の正式発表時期と CEO 人選
- NEDO 支援額の正式採択（2026 年下半期予定）と配分先
- 国内 GPU クラスタの調達先 — NVIDIA Vera Rubin プラットフォームを採用するか、国産チップ（ラピダス連携 ASIC など）に賭けるか
- Honda の二足歩行ロボット・自動運転車両との統合スケジュール
- Sony Mobility、Toyota Woven Planet との連携可能性
- 「データ主権」を法制化する次期 AI 推進法案（高市政権が秋の臨時国会で提出予定）
- 米国（特に Nvidia, OpenAI, Anthropic）との連携と排他のバランス — 完全な国内閉鎖は計算資源確保で現実的でない
