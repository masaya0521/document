# Anthropic vs Alibaba — 蒸留攻撃を巡る攻防

- **日付**: 2026-06-28
- **カテゴリ**: Tech
- **ソース**: [Nikkei Asia](https://asia.nikkei.com/business/technology/artificial-intelligence/anthropic-accuses-alibaba-of-largest-known-distillation-attack-on-claude), [Decrypt](https://decrypt.co/372130/anthropic-urges-congress-crack-down-ai-distillation-chinese-rivals), [Eastern Herald](https://easternherald.com/2026/06/27/anthropic-alibaba-claude-distillation-senate-sanctions/)

## 概要

Anthropic は2026年6月10日、米上院銀行委員会の Tim Scott 委員長と Elizabeth Warren 筆頭委員に宛てた書簡で、Alibaba およびその Qwen AI ラボに関連する事業者が「Anthropic が公表した中で過去最大のモデル蒸留キャンペーン」を実行したと主張した。約2.5万の不正アカウントを通じて2880万回超のやり取りを生成し、Claude の最も商業価値の高い能力を抽出しようとしたとされる。これを受け、米議会では中国 AI 競合への制裁を可能にする法案修正の動きが出ている。

## 詳細

### 「蒸留攻撃」とは

モデル蒸留（distillation）とは、強力な「教師モデル」の出力を大量に収集し、それを使って別の「生徒モデル」を訓練することで、教師モデルの能力を低コストで再現する手法。正規の用途もあるが、競合が API を通じて他社モデルの能力を不正に抽出する場合は知的財産の窃取とみなされる。攻撃者は「通常のユーザーと全く同じ使い方」をするため検知が難しいのが特徴。

### 攻撃の規模と手口

- **期間**: 2026年4月22日〜6月5日（約6週間）
- **規模**: 約25,000の不正アカウント、2880万回超のやり取り
- **標的能力**: エージェント的推論、ソフトウェアエンジニアリング能力、長期タスク完遂能力 — いずれもフロンティアモデルを旧世代と差別化する中核能力で、Anthropic がエンタープライズ向けの柱に据えているもの
- **回避手口**: Claude の中国アクセス制限を迂回するため、商用プロキシサービスで API 呼び出しの地理的発信元を秘匿

### 議会の反応

Bill Hagerty（共和・テネシー）と Andy Kim（民主・ニュージャージー）両上院議員は、敵対的な蒸留キャンペーンを行う事業者をブラックリスト化・制裁できる修正条項を、可決必至の国防関連法案に盛り込もうとしている。AI の知的財産保護が安全保障の論点として国家レベルで扱われ始めた。

### Alibaba の対応

報道時点で Alibaba は Reuters・CNBC・Bloomberg 等の取材に応じていない。

## 今後の注目点

- 国防法案修正が成立し、実際に制裁・ブラックリストが発動されるか
- 「API 経由の蒸留」をどう技術的・法的に立証・防御するかの枠組み議論
- 中国 AI ラボ（Qwen 等）の能力向上が蒸留にどこまで依存していたかの検証
- 米中 AI デカップリングの一段の進行と、API アクセス制限の強化
