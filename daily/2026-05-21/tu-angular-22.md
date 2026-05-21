# Angular 22 — Signal-First 時代の確立と Vitest デフォルト化

- **日付**: 2026-05-13（リリース）
- **カテゴリ**: Frontend
- **ソース**: [Angular Blog: Announcing v22](https://blog.angular.dev/announcing-angular-v22-feature-overview), [Angular v21 Release Event](https://angular.dev/events/v21), [HeroDevs: Angular Version History](https://www.herodevs.com/blog-posts/angular-version-history-every-release-date-support-window-and-end-of-life-date-from-angularjs-to-angular-22)

## 概要

Angular 22 が 2026 年 5 月 13 日にリリースされた。半年サイクルの定例メジャーアップデートだが、v22 は「Signal-First」体制への移行を実質完了させたバージョンとして位置づけられる。v20 で experimental だった Zoneless 変更検知は v21 でデフォルトとなり、v22 ではさらに踏み込んで `OnPush` がデフォルト化。同様に、v21 で experimental 公開された Signal Forms は v22 で stable に近づき、RxJS ベースの Reactive Forms から本格的に置き換わる準備が整った。

Angular 21 までで既に Vitest が Karma を置き換える形でテストランナーとして導入されていたが、v22 ではこれが本格的に既定となり、テスト実行が最大 10 倍程度高速化される構成へとさらに寄せられている。AI 連携面でも、v21 で導入された公式 MCP サーバ（Angular MCP Server）の活用が前提に組み込まれており、AI-native な開発フロー支援が強化されている。

## 主な変更点

### Signal Forms の stable 化への前進

- v21 で experimental だった Signal Forms が v22 で実プロダクト適用に耐える成熟度へ
- 巨大フォームの fine-grained 更新が可能（1 フィールド変更が他のフォームツリーに伝播しない）
- 深くネストしたフォームでもパフォーマンスが安定し、RxJS ベースよりも一貫した reactivity モデルを提供
- Reactive Forms / Template-driven Forms と当面は併存するが、新規開発は Signal Forms 推奨の路線

### Zoneless / OnPush デフォルト化

- v21 で Zoneless がデフォルトとなった流れを受け、v22 では `ChangeDetectionStrategy.OnPush` がデフォルトに
- Zone.js への依存をさらに薄くし、バンドルが軽量化
- クリック / タイマー単位の追跡が不要になり、変更検知サイクルが大幅に削減

### `debounced()` シグナル

- 「入力中は API を叩かず、ユーザーが止まったら発火する」用途を native に提供する debounced シグナルを導入
- ユーティリティ関数を別途書く必要がなく、Signal 中心の reactivity モデルにシームレスに統合

### Vitest デフォルト化

- Karma の段階的廃止を受けて、Vitest が新規プロジェクトのデフォルトテストランナーに
- ESM ネイティブ・並列実行・HMR 対応により、CI とローカル両方でテスト体験が改善
- 最大 10 倍程度のテスト実行高速化（Angular 公式ベンチ）

### TypeScript 5.9 サポート

- TypeScript 5.9 を正式サポート
- TypeScript 6.0 や、Go ベースのコンパイラを使う TypeScript 7.0 への移行準備の前段階にあたる

## 破壊的変更・移行ガイド

- **OnPush デフォルト化**: 既存プロジェクトでは新規生成コンポーネントが OnPush になるため、明示的にデフォルト変更検知を使い続けたい場合は設定を上書きする必要がある
- **Karma 廃止の進行**: Karma 設定を残しているプロジェクトは Vitest への移行が推奨される。Angular CLI には移行スクリプトが提供
- **Zone.js のさらなる縮退**: Zoneless 前提で書かれていない外部ライブラリと併用する場合、明示的に Zone.js を有効化する必要がある
- **Signal Forms と Reactive Forms の使い分け**: 既存 Reactive Forms は引き続き動作するが、新規実装では Signal Forms 推奨

## 今後の注目点

- Signal Forms の完全 stable 化（v23 以降想定、ただし v22 でも production 利用が始まる見込み）
- Zone.js 依存の完全廃止に向けたエコシステム整備
- TypeScript 7.0（Go ベースコンパイラ）への対応タイミング
- Angular MCP Server を活用した AI 連携機能の拡充
