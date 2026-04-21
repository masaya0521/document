# Node.js 26 — 現行リリースモデル最後のメジャーラインと次世代モデルへの橋渡し

- **日付**: 2026-04-21
- **カテゴリ**: Backend / Runtime
- **ソース**: [Evolving the Node.js Release Schedule](https://nodejs.org/en/blog/announcements/evolving-the-nodejs-release-schedule), [Upcoming Node.js Major Release (v26) #61832](https://github.com/nodejs/node/issues/61832), [Node.js Moves to Annual Major Releases (Socket)](https://socket.dev/blog/node-js-moves-to-annual-major-releases-starting-with-node-27)

## 概要

Node.js 26 は 2026-04-22 リリース予定で、**現行の偶数/奇数リリースモデル下で提供される最後のメジャー**となる。2026-03-22 までに main に入った変更がリリースに含まれる。

同時に、Node.js プロジェクトは 27 以降のリリースモデルを刷新することを発表しており、26 は「旧モデル最後のメジャー」であると同時に「27 以降の新モデルへの移行準備リリース」でもある。

Node.js 26 の LTS 昇格は 2026-10 を予定しており、従来どおり「偶数メジャー → LTS」の経路をたどる。

## 主な変更点

### リリース時点の主要機能トピック

2026-03-22 の機能凍結までに landing した内容が対象になる。主なテーマは以下（詳細は 22 日の changelog 確定待ち）。

- ネイティブ TypeScript サポートの継続的な成熟
- パフォーマンス系：V8 アップデート、fetch / HTTP 層の最適化
- Permission Model の周辺 API 拡充
- セキュリティ関連の強化と legacy API の削除

Node.js 24 LTS で導入された方向性（ネイティブ TS、Permission Model）を延長する形でメジャーバージョンアップが行われる。

### 現行モデル下の位置づけ

- Node.js 26: 2026-04-22 リリース、2026-10 に LTS 昇格予定
- Node.js 27: 新モデルに移行。2026-10 から alpha チャネルで提供され、2027-04 に Current、2027-10 に LTS

## 破壊的変更・移行ガイド

メジャーバージョンアップのため、以下のような変更が予想される（一般的な Node.js メジャー更新に共通するパターン）。

- 古い OpenSSL のサポート終了に伴う暗号化 API の挙動変更
- deprecated マークされていた API の削除（`util._extend` 系、legacy url API、古い Buffer コンストラクタなど過去のパターン）
- V8 の新バージョン採用に伴う JavaScript 挙動の微小変化（エラーメッセージ形式、stack trace）

本番環境への導入は **LTS 昇格（2026-10 予定）を待つ**のが一般的な運用パターン。新規開発や実験的な評価であれば、4 月リリース直後から入れても良い。

## 次期モデル（Node.js 27 以降）のポイント

Node.js 27 から以下のリリースモデル変更が適用される。

1. **年 1 回のメジャーリリース**: 年 2 回 → 年 1 回に集約（4 月リリース）
2. **全メジャーが LTS**: 奇数番号をスキップするのではなく、すべての年次リリースが LTS 化
3. **バージョン番号が年と揃う**: Node.js 27 → 2027 Current、Node.js 28 → 2028 Current
4. **Alpha チャネル**: Current 前に 6 ヶ月の alpha 期間を設け、早期検証機会を提供
5. **サポート期間**: 初回 Current から EOL まで合計 36 ヶ月

背景には、Chrome / Firefox 等のブラウザが高速リリース化している流れとの整合性、および「偶数 / 奇数」の分かりづらさを解消する目的がある。Node.js 26 はこの大転換の直前に出るリリースという意味でも節目になる。

## 今後の注目点

- **2026-04-22**: Node.js 26 正式リリース、詳細 changelog 確定
- **2026-10**: Node.js 26 LTS 昇格、同時に Node.js 27 alpha チャネル開始
- **TS ランタイム競合**: Deno 2.5、Bun 1.3.13 が 4 月に同時期リリース。3 ランタイムすべてがネイティブ TS サポートと高速起動を武器に競合する構図が本格化
- **エンタープライズ運用**: 「全メジャーが LTS」になることで、偶数だけ本番採用という従来パターンが変わる。社内ポリシーを更新する組織が出てくる見込み
- **20 系・22 系からの移行**: Node.js 20 は 2026-04-30 に EoL、22 系から直接 26 系へスキップするか、24 LTS を経由するかの判断が 2026 Q2 の焦点
