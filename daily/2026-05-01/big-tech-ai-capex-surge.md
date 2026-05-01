# Big Tech Q1 capex $130B — AI インフラ軍拡競争の現在地

- **日付**: 2026-05-01
- **カテゴリ**: Tech
- **ソース**: [CNBC](https://www.cnbc.com/2026/04/30/google-microsoft-and-amazon-all-report-cloud-beats-in-earnings.html) / [HeyGoTrade (Microsoft Q1)](https://www.heygotrade.com/en/blog/microsoft-q1-2026-earnings-reaction/) / [Fortune](https://fortune.com/2026/04/29/microsoft-meta-google-ai-capex-spending-billions/) / [Directions on Microsoft](https://www.directionsonmicrosoft.com/microsoft-q1-fy26-earnings-cloud-supply-constraints-to-last-through-at-least-june-2026/)

## 概要

2026 年 4 月最終週、Alphabet・Meta・Microsoft・Amazon の 4 社が Q1 決算を発表し、設備投資（capex）が四半期だけで $130B を超えた。通年見通しは合計で **$725B 規模**まで膨らみ、四半期ベースでも前期に続いて過去最高を更新。AI インフラへの「軍拡競争」がついにマクロ経済を動かす規模に達したことが鮮明になった一方、Microsoft が「Azure は容量不足が FY26 末まで継続」と認めるなど、需要超過の構造的課題も同時に表面化している。

クラウド事業は、Google Cloud +63%、Azure +40%、AWS +28% と 3 社揃って加速し、契約バックログは Microsoft $392B、Google $462B と 1 兆ドル規模に近づいている。Bedrock のトークン処理量は「過去全期間の合計を 1 四半期で超えた」とされ、AI ワークロードの実需が急成長していることが裏付けられた。

## 詳細

### 通年 capex ガイダンス

| 企業 | 通年 capex 見通し | 主な変化 |
|------|------------------|---------|
| Microsoft | **$190B**（初公表） | Alphabet と並ぶ規模。FY26 末（2026/6 末）まで「容量不足」継続を明言 |
| Alphabet | $185B 規模に上方修正 | Google Cloud のバックログがほぼ倍増 |
| Meta | $125–145B → さらに上方修正 | Q1 売上 $56.3B（+33%）も capex 増で時間外 -5.7% |
| Amazon | $200B（据え置き） | AWS 関連 AI サービスのランレートは $15B 超 |
| **合計** | **約 $725B** | 業界全体で「マクロに効く規模」へ |

Q1 単独で見ると 4 社合計の capex は $130B 超に達した。これは前年比でも +50% 超のペースで、「2026 年は AI インフラ投資の年」という見立てが数字で裏付けられた格好。

### Azure の "供給制約"

Microsoft の Q1 FY26 決算で最も強調されたのは、Azure AI 容量が需要に追いついていないという供給側の限界だ。

- Azure 売上は +40% で予想を上回ったが、CFO Amy Hood は「私たちは何四半期も供給不足で、追いつくと思っていたが、追いつかない。需要は増え続けている」と述べた。
- 容量制約は **FY26 末（2026 年 6 月）まで続く**見通しで、データセンターの電力・冷却・GPU 入手の各面でボトルネックが発生。
- 商業バックログは $392B（前年比 +51%）に積み上がり、需要側のキューがさらに膨張中。

つまり「金を積めば即拡張できる」局面はすでに過ぎており、土地・電力・サプライチェーンといった**物理層の制約**が AI 経済の律速になりつつある。SoftBank が Roze AI（DC 建設ロボティクス）を立ち上げて IPO まで視野に入れたのは、まさにこの物理層ボトルネックを狙い撃ちにした動きである。

### Wall Street の評価分岐

Fortune は「Microsoft、Meta、Google が AI 支出を増額したが、投資家を納得させられたのは Google だけ」と報じている。

- **Google**: Cloud +63%、バックログ倍増、AI 検索広告の貢献も鮮明 → 株価は好感
- **Microsoft**: 容量制約の明示が「金を積んでも捌ききれていない」というネガに転化
- **Meta**: 売上は伸びたが capex 増額が嫌気され時間外 -5.7%

差を分けたのは「投じた capex が売上に変換されているか」というユニットエコノミクスの説得力だった。Google Cloud のマージン拡大が突出していた点も投資家の判断を後押ししたとみられる。

### AWS / Bedrock の急加速

AWS は売上 +28%（過去 15 四半期で最速）、営業利益 +23% で Street コンセンサスを大きく上振れ。

- Bedrock のトークン処理量は **2026 Q1 が 2025 年通年累計を超える**規模に到達
- Bedrock 顧客支出 QoQ +170%
- Trainium 年商ランレート $20B 超で 3 桁成長継続

これにより AWS は「Anthropic / Bedrock」軸での AI クラウド勝者として、Azure（OpenAI）と Google Cloud（Gemini）に並ぶ第三極を確立した。

## 今後の注目点

- **電力契約と土地確保**: 2026 年後半は capex の絶対額より「電力契約・原子力 PPA・送電網拡張」が成長の制約解除の鍵に。Microsoft は SMR / 既存原発 PPA を複数結んでおり、他社の追随ペースに注目。
- **半導体配分**: NVIDIA Blackwell / Rubin 世代の出荷配分が、各社の供給制約を解消できるか。Trainium / TPU など内製チップの比率拡大も続く。
- **ROI の検証**: 通年 capex $725B が 2027 年以降の売上・利益に変換できるかが、米国株の AI トレード継続可否を決める最大の論点。Google Cloud のマージン拡大が他社に波及するかを四半期ごとに追う必要がある。
- **マクロ波及**: AI インフラ投資が GDP 寄与（米 Q1 +2%）の半分を占めるとの試算もあり、設備投資ピーク後の反動リスクが景気循環の重大変数に。
- **規制・地政学**: 中国向け輸出規制、データセンターへの州税優遇打ち切り、電力配分を巡る訴訟など、政治的なボトルネックも増加中。
