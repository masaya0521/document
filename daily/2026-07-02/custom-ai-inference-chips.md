# 自社推論チップ競争と Nvidia 依存からの脱却

- **日付**: 2026-07-02
- **カテゴリ**: Tech
- **ソース**: [OpenAI and Broadcom unveil LLM-optimized inference chip（OpenAI）](https://openai.com/index/openai-broadcom-jalapeno-inference-chip/) / [Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/broadcom-and-openai-unveil-custom-built-jalapeno-inference-processor-openais-first-chip-is-a-massive-reticle-sized-asic-built-in-an-ultra-fast-nine-month-development-cycle)

## 概要

OpenAI は Broadcom と共同開発した初の自社推論チップ「Jalapeño」を発表した。推論（学習済みモデルをユーザー要求に応じて実行する処理）に特化した ASIC で、現行の最先端品より優れた電力あたり性能を示すとされる。Google の TPU、Amazon の Trainium に続き、主要 AI プレイヤーが自社シリコンで Nvidia 一社依存を減らす流れが鮮明になっている。同じ流れの中で、OpenAI は「Jalapeño」計画を、Apple・SpaceX なども取り組むカスタムチップ競争の一角として公にしている。

## 詳細

### Jalapeño の位置づけ

- **用途は推論に特化**: 事前学習のような負荷の高い処理は引き続き Nvidia ハードウェアに依存する見込み。役割分担型のアプローチ。
- **異例の開発速度**: テープアウトまで約 9 ヶ月というきわめて速い ASIC 開発サイクルで、OpenAI 自身のモデルを設計に活用したとされる。レチクルサイズの大型 ASIC。
- **展開時期**: 2026 年後半に初期展開予定。複数世代にわたる計算プラットフォームの第一歩と位置づけられる。
- **経済性が本質**: 一部報道は「Nvidia の物語ではなく、ユニットエコノミクス（単価構造）の物語」と評し、推論コストを大幅に下げる狙いを強調する。

### 競争環境

Google（TPU）と Amazon（Trainium）は長年にわたり成熟したカスタムシリコンプログラムを運用してきた。OpenAI はここに参入しつつ、2026 年 2 月に Nvidia が OpenAI へ 300 億ドルを直接投資し 10GW 規模の計算システム導入で合意した経緯もあり、学習用途では Nvidia との提携を維持したまま推論用途を内製化する構図となっている。

### 供給制約という追い風

同時期には、Google が計算リソース逼迫を理由に Meta など複数顧客の Gemini 利用を制限し、SpaceX からクラウド容量を追加調達する契約も報じられた。GPU 供給がボトルネックとなる中、自社シリコンによる推論コストと供給の内製化は各社の共通課題になっている。

## 今後の注目点

- Jalapeño の実機性能（電力あたり性能・実効スループット）が公表値通りか、late-2026 の展開で検証される
- 推論の内製化がクラウド各社（AWS/Google/Azure）の AI 課金モデルに与える価格圧力
- Nvidia の推論市場シェアがカスタム ASIC の台頭でどう推移するか
- Broadcom を軸とした「ハイパースケーラー向けカスタム ASIC」ビジネスの拡大
- 学習は Nvidia・推論は自社という役割分担が定着するか、あるいは自社シリコンが学習領域にも広がるか
