# Anthropic Claude Mythos と Project Glasswing — AI がサイバーセキュリティを根本から変える

- **日付**: 2026-04-15
- **カテゴリ**: Tech
- **ソース**: [The Hacker News](https://thehackernews.com/2026/04/anthropics-claude-mythos-finds.html), [Anthropic](https://www.anthropic.com/glasswing)

## 概要

Anthropic は2026年4月7日、フロンティアモデル Claude Mythos Preview を発表した。このモデルは全主要 OS・ブラウザにおいて数千件のゼロデイ脆弱性を自律的に発見・悪用する能力を実証し、サイバーセキュリティの根本的なパラダイムシフトを引き起こしている。同時に Anthropic はこの能力を防御目的に活用するための業界横断イニシアチブ「Project Glasswing」を発足させた。

## 詳細

### Mythos の脆弱性発見能力

Claude Mythos Preview は、人間のトップレベルセキュリティ研究者に匹敵またはそれを超える脆弱性発見能力を持つ。特筆すべき事例として、FreeBSD の NFS 実装に17年間潜んでいたリモートコード実行脆弱性（CVE-2026-4747）を完全自律的に発見・悪用した。この脆弱性は未認証のインターネット上の攻撃者がサーバーの完全な制御権を取得可能な深刻なものだった。

Anthropic はこのモデルについて「最も熟練した人間以外にはマッチできないレベルのコーディング能力を持ち、ソフトウェアの脆弱性を発見・悪用できる」と述べている。

### Project Glasswing の構成

Anthropic はこれらの能力が悪用されるリスクを踏まえ、Mythos を一般公開せず、限定的な防御利用に限定する Project Glasswing を立ち上げた。

**参加企業・組織:**
- クラウド: AWS、Google、Microsoft
- セキュリティ: CrowdStrike、Palo Alto Networks、Cisco
- ハードウェア: Apple、NVIDIA、Broadcom
- 金融: JPMorgan Chase
- OSS: Linux Foundation

Anthropic は Mythos Preview の利用クレジットとして最大1億ドル、オープンソースセキュリティ組織への直接寄付として400万ドルを拠出する。

### 「Glasswing パラドックス」

Forrester や Picus Security が指摘する「Glasswing パラドックス」は本質的な問題を提起している。すべてを破壊できるものが、すべてを修復するものでもあるという矛盾だ。Mythos の能力は防御に使えば重大な脆弱性を事前に修正できるが、同様の能力が悪意ある行為者に渡れば壊滅的な攻撃が可能になる。

Palo Alto Networks は、類似の能力が数週間〜数ヶ月以内に他のモデルにも拡散する可能性を警告しており、防御側が先行するための時間的猶予は限られている。

### IBM の反応とオープンソースへの影響

IBM は「Open Source, After Mythos」と題した声明を発表。AI がこの閾値を超えた今、オープンソースにおける「開放性」はイデオロギーではなく実用的な問題になったと指摘。脆弱性の発見と修正のサイクルが AI によって劇的に加速される世界では、オープンソースのコード透明性がむしろセキュリティ上の利点になるという議論を展開している。

## 今後の注目点

- **能力の拡散速度**: Palo Alto Networks が警告する通り、類似能力が他の AI モデルに拡散するまでのタイムライン。防御側の先行投資期間がどれだけ確保できるか
- **Glasswing の実効性**: 限定公開モデルによる防御アプローチが、実際にクリティカルソフトウェアの脆弱性修正にどれだけ貢献するか
- **規制への影響**: AI のサイバー攻撃能力に対する各国の規制対応。特に EU AI Act やバイデン政権の AI 行政命令との整合性
- **オープンソースセキュリティ**: Chainguard EmeritOSS と合わせ、放棄された OSS プロジェクトの脆弱性を AI で検出・修正するワークフローの確立
- **レッドチームの再定義**: 人間のペネトレーションテスターの役割が AI によってどう変化するか。セキュリティ人材市場への影響
