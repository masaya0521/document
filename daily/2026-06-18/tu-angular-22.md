# Angular 22 — signal-first 時代へ

- **日付**: 2026-06-18（Angular 22 リリース: 2026-06-03）
- **カテゴリ**: Frontend
- **ソース**: [Angular 22 Is Here (dev.to)](https://dev.to/rigole/angular-22-is-here-everything-you-need-to-know-4g3c), [endoflife.date/angular](https://endoflife.date/angular)

## 概要

Angular 22 は「signal-first」を掲げたメジャーリリースで、Angular 21 で実験的に導入された Signal ベースの機能群が軒並み安定化した。最大の変更は **変更検知のデフォルトが OnPush になった** ことで、従来の暗黙的なフルツリー変更検知から、シグナル駆動のきめ細かい更新へとフレームワークの既定姿勢がシフトした。`ng update` による自動マイグレーションが用意されているため、既存アプリも比較的スムーズに移行できる。

## 主な変更点

- **OnPush がデフォルト変更検知に**: 旧来の "Default" 戦略は "Eager" に改名され非推奨化。`ng update` 実行時、既存の非 OnPush コンポーネントは自動で "Eager" に設定され、挙動の互換性が保たれる。
- **Signal Forms の安定化**: 実験的だった Signal ベースのフォームが production-ready に。冗長な `FormGroup` / `FormControl` のパターンを、深くネストしたシグナル構造でフォーム状態を表現する `form()` 関数に置き換えられる。
- **Resource API の安定化**: `resource()` / `rxResource()` / `httpResource()` が安定版に。レースコンディションやローディング状態の扱いをテンプレート内で自動処理し、データフェッチを簡潔に書ける。
- **`@Service` デコレータ**: 頻出の `@Injectable({ providedIn: 'root' })` を `@Service()` で置き換え可能。`autoProvided` オプションでカスタム構成も可能。
- **`injectAsync`**: 依存を必要になったときだけ遅延ロードするプリミティブ。重い機能特化サービスの起動性能を改善。
- **`debounced()` シグナル**: シグナルに遅延を付与するユーティリティ。検索入力などで手動の RxJS debounce が不要に。

## 破壊的変更・移行ガイド

- 主要な破壊的変更は **OnPush がデフォルト** になった点。`ng update` が既存コンポーネントを新しい "Eager" 戦略に設定して自動移行するため、影響は最小化される。ただし、これまで暗黙の変更検知に依存していたコンポーネント（外部ミューテーションで状態を変えていた箇所など）は、移行後に「Eager」へ固定されるため、シグナル化を進める良い機会となる。
- "Default" → "Eager" の改名と非推奨化に伴い、明示的に `ChangeDetectionStrategy.Default` を指定していたコードは見直しが必要。

## 今後の注目点

- Signal Forms / Resource API の安定化により、RxJS 依存を減らした signal 中心のアーキテクチャがコミュニティの標準になっていくか。
- OnPush デフォルト化を機に、既存の大規模アプリでパフォーマンス改善（不要な再レンダリング削減）がどの程度得られるか。
- `@Service` や `injectAsync` など DI 周りの簡素化が、今後の zoneless 化（Zone.js 撤廃）とどう連動していくか。
