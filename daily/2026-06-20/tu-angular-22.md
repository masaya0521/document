# Angular — v22

- **日付**: 2026-06-03（リリース）
- **カテゴリ**: Frontend
- **ソース**: [DEV: Angular 22 Is Here](https://dev.to/rigole/angular-22-is-here-everything-you-need-to-know-4g3c), [Bacancy: Angular 22](https://www.bacancytechnology.com/blog/angular-22)

## 概要

Angular 22 は、近年進めてきた Signals ベースのリアクティビティと Zoneless アーキテクチャへの移行を一つの大きな節目として完成させたメジャーリリース。最大の変更は **変更検出戦略のデフォルトが `OnPush` になった**ことで、これは破壊的変更にあたる。あわせて Signal Forms と Resource API が実験段階を卒業して本番対応となり、Signals 中心のアプリ設計が「標準的な書き方」として確立された。

従来の手続き的なフォーム・RxJS 多用のパターンから、宣言的・Signal 駆動のパターンへ移行する流れが一段と明確になっている。

## 主な変更点

### 変更検出のデフォルトが OnPush に（破壊的変更）

- 従来の `Default` 戦略は廃止され、`OnPush` 相当が新しいデフォルトに。
- Signal と組み合わせることで、依存している値が変化したときだけ精密に再レンダリングされる。
- 既存コンポーネントは `ng update` 実行時に自動移行される。手動で `Default` に依存していたコードは挙動を確認する必要がある。

### Signal Forms の本番対応

- 実験段階を卒業しプロダクション利用可能に。
- `form()` 関数により、冗長な `FormGroup` / `FormControl` のボイラープレートが不要に。
- ネストした Signal 構造で各プロパティの状態（値・バリデーション・dirty 等）を管理。

### Resource API の安定化

- `resource`、`rxResource`、`httpResource` が本番対応。
- 非同期データ取得でレース条件を自動処理（`switchMap` 相当の挙動）。
- テンプレートと自動同期し、ローディング/エラー状態を Signal として扱える。

### DI まわりの新機能

- **`@Service` デコレータ**: `@Injectable({ providedIn: 'root' })` の簡潔な代替。デフォルトでルート提供、`autoProvided: false` で除外可能。
- **`injectAsync`**: 依存を必要になった時点で遅延ロード。大型サービスや機能固有依存の効率管理に有用。

### その他

- **`debounced()` Signal**: 検索入力など高頻度イベントの遅延通知を Signal レベルで実現。RxJS の手動 `debounceTime` が不要に。
- インクリメンタルハイドレーションがデフォルト有効化され、SSR 配信が高速化。
- プラットフォーム全体のセキュリティ強化。

## 破壊的変更・移行ガイド

- **OnPush デフォルト化**: 最大の注意点。`ng update` による自動移行が用意されているが、`Default` 戦略前提で「いつの間にか再レンダリングされていた」コードは、Signal もしくは明示的な `markForCheck()` への置き換えが必要になる場合がある。
- 既存の `FormGroup`/`FormControl` ベースのフォームはそのまま動作するが、新規実装では Signal Forms（`form()`）が推奨パスとなる。
- 段階的移行が可能な設計のため、Resource API・Signal Forms は既存コードと共存させながら部分導入できる。

## 今後の注目点

- Signal 中心設計が「デフォルト」になったことで、コミュニティのベストプラクティスやライブラリ側の対応がどこまで追従するか。
- Zoneless（zone.js 非依存）構成の本番採用事例の蓄積。
- Resource API がデータフェッチライブラリ（TanStack Query 等）の利用パターンにどう影響するか。
