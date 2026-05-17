# Google + SpaceX 軌道データセンター構想 (Project Suncatcher)

- **日付**: 2026-05-18
- **カテゴリ**: Tech
- **ソース**: [TechCrunch](https://techcrunch.com/2026/05/12/report-google-and-spacex-in-talks-to-put-data-centers-into-orbit/) / [Bloomberg](https://www.bloomberg.com/news/articles/2026-05-12/google-in-talks-to-use-spacex-to-launch-space-data-centers-wsj) / [DataCenterDynamics](https://www.datacenterdynamics.com/en/news/google-in-talks-with-spacex-regarding-suncatcher-orbital-data-center-project/)

## 概要

Google が AI 学習・推論用コンピュートを地上から軌道に移す「**Project Suncatcher**」について、SpaceX を打ち上げパートナー候補として早期協議に入っていると Wall Street Journal が報じた。Suncatcher は 2025 年末に Sundar Pichai が公表した「ムーンショット」プロジェクトで、太陽光駆動・Google の TPU を搭載した約 81 基の衛星を 1km 半径の編隊に展開し、軌道上で AI 計算クラスタを構成することを構想している。SpaceX は 2026 年後半に 1.75 兆ドル規模の IPO を準備しており、「軌道は AI コンピュートの最安拠点になる」というストーリーを投資家に提示している。

## 詳細

### 構想の枠組み

- **衛星設計パートナー**: Planet Labs と提携し、2027 年初頭に試作衛星 2 基を打ち上げる計画。
- **コンピュート**: 各衛星に Google の Tensor Processing Unit (TPU) を搭載。光リンクで衛星間を接続し、編隊全体で 1 クラスタを構成する想定。
- **電源**: 太陽光発電。地上データセンターのボトルネックである電力・冷却・水資源・地域反発を回避できる点が訴求材料。
- **打ち上げ**: SpaceX の Starship を主候補としつつ、Google は他社（Blue Origin、Rocket Lab、Stoke Space など）とも並行協議中。排他契約には至っていない。

### 背景となる地上側の課題

Gallup 調査では米成人の 71% が「居住地域に AI データセンターを建てること」に反対しており、48% が「強く反対」と回答した。電力網逼迫・水資源枯渇・固定資産税優遇の批判など、地上の AI インフラ拡張は社会的逆風が強まっている。これに対し軌道では:

- **電力**: 太陽光が遮蔽されない軌道で発電効率が高く、24 時間連続稼働が可能。
- **冷却**: 真空中での放射冷却を利用、地上の水冷インフラ不要。
- **規制**: 地方自治体・住民との合意形成が不要。
- **遅延**: 一方で、地上ユーザとの往復遅延・大気減衰によるバンド幅・地上局運用コストが新たなボトルネック。

### コスト現実

TechCrunch / Bloomberg はそろって「現時点の打ち上げ＋衛星製造コストを織り込むと、軌道データセンターは地上より割高」と指摘。SpaceX の主張は「Starship が量産・再使用化されれば打ち上げコストは桁違いに下がる」「軌道発電は限界費用が低い」という前提に依存しており、シナリオの蓋然性は依然議論の的。

### 関連する動き

- **Anthropic + SpaceX**: 2026 年 5 月初旬に Anthropic が SpaceX 傘下 xAI のメンフィスデータセンターを利用する契約を締結。将来的に軌道協業も視野（SpaceX は 2026 年 2 月に xAI を買収）。
- **Anthropic + Akamai**: 別途 18 億ドル規模のエッジコンピュート契約。AI 大手は「単一ハイパースケーラー依存」から複数のコンピュート供給網へ分散しつつある。
- **ハイパースケーラー capex**: Meta・Amazon・Microsoft・Alphabet の 2026 年合算 capex は 7,250 億ドル超（前年比 +75% 超）に達し、地上 + 軌道のハイブリッド構想が現実味を帯びる規模感に。

## なぜ重要か

1. **地上 capex ピークの示唆**: 2026 年の AI 投資ブームが「軌道に逃げる」必要があるほど地上の制約に直面しているという市場からのシグナル。
2. **電力 vs. 計算のトレードオフ再定義**: AI スケーリング則の制約はもはやチップではなく電力。再生可能エネルギー単一の前提（太陽光 + 軌道）への賭けが本格化する。
3. **規制裁定**: 軌道インフラは国家規制・地方政治を越えやすい一方、宇宙ゴミ・周波数調整・国際法（OST, ITU）の論点が新たに浮上。
4. **垂直統合**: SpaceX (打ち上げ + xAI) × Google (TPU + Suncatcher) × Anthropic (推論需要) の三角関係が示すように、「コンピュート × 打ち上げ × モデル」のフルスタック統合競争が始まりつつある。

## 今後の注目点

- **2027 年初頭の Suncatcher 試作機 2 基打ち上げ成否**: 軌道間光通信・熱設計・TPU の宇宙耐性の実証。
- **Starship の運用安定化**: 軌道データセンター経済性の前提となる「打ち上げコスト/kg」の実績値。
- **SpaceX IPO 投資家のストーリー消化**: 1.75 兆ドル評価の根拠として軌道コンピュートがどこまで織り込まれるか。
- **競合動向**: Amazon (Project Kuiper)、Microsoft (Azure Space)、中国勢 (Guowang / Qianfan) の軌道 AI 計画。
- **国際規制**: 宇宙ゴミ・周波数調整・宇宙活動法（米国 / 日本 / EU）における「軌道計算インフラ」の位置付け。
- **冷却・放熱の物理的上限**: 真空冷却が現実的に支えられるラック密度（kW/サット）の限界。
