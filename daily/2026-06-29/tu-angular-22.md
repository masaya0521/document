# Angular — v22（signal-first と Selectorless Components）

- **日付**: 2026-06-29
- **カテゴリ**: Frontend
- **ソース**: [Angular Releases (GitHub)](https://github.com/angular/angular/releases), [Angular 公式リリースポリシー](https://angular.dev/reference/releases), [Angular endoflife.date](https://endoflife.date/angular)

## 概要

2026 年 6 月 3 日、Angular 22 がリリースされた。Angular 20 以降続いてきた Signals（シグナル）中心への移行が一段と進み、22 は「signal-first」時代を本格化させるメジャーバージョンと位置づけられている。最大の目玉は **Selectorless Components**（セレクタレスコンポーネント）で、コンポーネントをセレクタ文字列なしにテンプレートへ直接 import して利用できるようになり、コンポーネント合成のボイラープレートが削減される。

サポート期間は、Active support が 2026 年 12 月まで、LTS が 2028 年 5 月まで。直前の Angular 21（2025 年 11 月）は LTS が 2027 年 5 月までとなっている。

## 主な変更点

- **Selectorless Components**: テンプレート内でコンポーネント / ディレクティブをセレクタ文字列を介さず直接 import して使用できる。`@Component` の `selector` や `imports` 配列の記述負担が減り、依存関係がコード上で追いやすくなる。
- **signal-first の徹底**: 状態管理・変更検知のデフォルト経路として Signals を前提とした API・パターンが中心に。`@Input`/`@Output` のシグナルベース API やゾーンレス（zoneless）変更検知の流れと整合する。
- バンドルサイズ・パフォーマンスの継続的改善（Signals ベース化に伴う不要な再レンダリング削減）。

## 破壊的変更・移行ガイド

- Angular はメジャーごとに `ng update` による自動マイグレーション（schematics）を提供しているため、まずは `ng update @angular/core@22 @angular/cli@22` を実行し、提示される移行スクリプトに従うのが基本。
- Selectorless への移行は任意。既存のセレクタベースのコンポーネントはそのまま動作するため、新規コンポーネントから段階的に採用できる。
- zoneless / signal ベースへ寄せる場合は、ZoneJS 依存のサードパーティライブラリの互換性を事前に確認すること。

## 今後の注目点

- Selectorless が普及した際の、エディタ補完・テンプレート型チェック・ツールチェーンの成熟度。
- signal-first 化により、NgRx 等の既存状態管理ライブラリの位置づけがどう変わるか。
- Angular 23（次期）に向けた zoneless のデフォルト化の動向。
