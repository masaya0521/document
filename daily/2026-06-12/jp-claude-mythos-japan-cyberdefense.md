# 日本政府・3メガバンクが Claude Mythos アクセス権を取得 — Project Glasswing 拡大の文脈

- **日付**: 2026-06-12
- **カテゴリ**: Japan Tech
- **ソース**: [ITmedia NEWS](https://www.itmedia.co.jp/news/articles/2606/04/news073.html) / [Anthropic](https://www.anthropic.com/news/expanding-project-glasswing) / [Ledge.ai](https://ledge.ai/articles/anthropic_mythos_japan_megabanks_financial_cybersecurity)

## 概要

Anthropic は6月2日、サイバーセキュリティ防衛プロジェクト「Project Glasswing」を拡大し、Claude Mythos（Claude Mythos Preview）へのアクセス権を15カ国以上・約150団体に新たに付与すると発表した。この拡大に日本政府が含まれており、松本尚デジタル大臣が6月3日の臨時閣議後会見で政府のアクセス権取得を発表。片山金融相も政府・大手金融機関への付与を「非常に喜ばしい」と表明した（[日経](https://www.nikkei.com/article/DGXZQOUB223F00S6A520C2000000/)）。

金融機関側では三菱UFJ銀行・三井住友銀行・みずほ銀行の3メガバンクが6月中にもアクセス権を取得する見込みと報じられており（[日経](https://www.nikkei.com/article/DGXZQOUB130SI0T10C26A5000000/)）、官民で金融システム・重要インフラのサイバー防衛に活用する体制が動き出した。

## 詳細

### Project Glasswing とは

Project Glasswing は、フロンティアモデル Claude Mythos Preview の脆弱性発見能力を「世界で最も重要なソフトウェアの防御」に振り向ける Anthropic 主導の協調プロジェクト（[公式ページ](https://www.anthropic.com/glasswing)）。

- Mythos Preview は、ソフトウェア脆弱性の発見・悪用において「最も熟練した人間以外のすべてを上回る」水準のコーディング能力を持つとされる
- 立ち上げ後、Anthropic と約50の初期パートナーは、主要な OS・ブラウザを含む基幹ソフトウェアで1万件超の high / critical 深刻度の脆弱性を発見済み（[Anthropic 中間報告](https://www.anthropic.com/research/glasswing-initial-update)）
- 今回の拡大で対象は約150団体増え、電力・水道・医療・通信などの重要インフラ事業者が加わった（[Cybersecurity Dive](https://www.cybersecuritydive.com/news/ai-anthropic-claude-mythos-project-glasswing-expand/821714/)）

攻撃側にも使えてしまう能力（デュアルユース）を、承認された防御側組織に限定提供することでバランスを取る、という設計が特徴。一般提供版の Claude Fable 5 とは異なり、Mythos は承認組織限定で提供される。

### 日本側の受け入れ体制

- **政府**: 内閣サイバーセキュリティ関連部局を中心に、政府機関システムの脆弱性診断・サイバー防衛強化に活用する方針。OpenAI・Google・Microsoft とも同様の協議を進めるとされる（[ITmedia](https://www.itmedia.co.jp/news/articles/2606/04/news073.html)）
- **金融**: 3メガバンクが金融システム防衛の観点でアクセス権を取得へ。勘定系・決済システムなど社会インフラ級のソフトウェア資産を抱える金融機関にとって、フロンティアモデルによる事前の脆弱性発見は防御側の大きな武器になる（[Ledge.ai](https://ledge.ai/articles/anthropic_mythos_japan_megabanks_financial_cybersecurity)）

なお、能動的サイバー防御の法整備を進めてきた日本にとって、海外フロンティアモデルへの依存と国内体制整備のバランスは今後の論点になる。

### なぜ重要か

「AI が脆弱性を見つける速度が人間のパッチ適用速度を上回る」時代の到来を、政府・金融という社会基盤レベルで前提にし始めたことを意味する。防御側がフロンティアモデルを先に回す体制が整わなければ、同等の能力を持つ攻撃者に対して構造的に不利になる——という認識が、今回の官民同時の動きの背景にある。

## 今後の注目点

- 3メガバンクの正式なアクセス権取得時期と、脆弱性発見の運用体制（自行内での検証フロー、当局への報告ルール）
- 政府の活用範囲: 政府機関システムの診断にとどまるか、重要インフラ事業者への横展開まで広がるか
- OpenAI・Google・Microsoft との協議の行方（マルチベンダー体制になるか）
- Mythos が発見した脆弱性の開示・修正プロセス（責任ある開示の枠組み）が日本国内でどう整備されるか
- 国内ベンダー・SIer のセキュリティ診断ビジネスへの影響
