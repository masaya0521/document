# Angular 22 — Signal Forms / Resource API 安定化と OnPush デフォルト化

- **日付**: 2026-06-10（リリース: 2026-06-03）
- **カテゴリ**: Frontend
- **ソース**: [Angular Architects](https://www.angulararchitects.io/en/blog/angular-22-the-most-important-new-features-at-a-glance/), [Ninja Squad — What's new in Angular 22.0](https://blog.ninja-squad.com/2026/06/03/what-is-new-angular-22.0)

## 概要

Angular 22 が 2026年6月3日にリリースされた。数バージョンにわたって experimental だった主要 API がまとめて安定化する「集大成（consolidation）」リリースで、**Signal Forms** と **Resource API** が production-ready になった。あわせて変更検知のデフォルトが **OnPush** に切り替わり、Incremental Hydration がデフォルト有効化されるなど、「Signal ベースのリアクティブ Angular」が標準形として固まった節目となる。

破壊的に見える挙動変更（OnPush デフォルト化、Fetch backend デフォルト化）も、`ng update` が後方互換を保つようマイグレーションを自動挿入するため、既存アプリは段階的に移行できる。

## 主な変更点

### Signal Forms が安定化

experimental だった Signal Forms が stable に昇格。実務で必要な周辺機能が揃った。

- **Submission API**: サーバーサイドバリデーションとの統合
- **`FormRoot` ディレクティブ**: ネイティブ `<form>` のハンドリング
- **動的スキーマ**: `validateStandardSchema` による Standard Schema バリデーション
- **CSS クラス制御**: Reactive Forms と同等の状態連動クラス付与
- **相互運用**: 既存 Reactive Forms コントロールとの interop

### Resource API が安定化

`resource` / `rxResource` / `httpResource` が stable に。非同期データ取得を Signal で宣言的に扱える。あわせて `debounced` 関数が追加され、指定遅延で値を更新する Resource を生成できる。

### OnPush がデフォルトの変更検知戦略に

```ts
// Angular 22 以降、明示指定がなければ OnPush 相当で動作
@Component({ /* changeDetection 未指定 → OnPush */ })
```

`ng update` 実行時は既存コンポーネントに `ChangeDetectionStrategy.Eager`（従来挙動）を自動付与するため、アップグレード直後の挙動変化を防ぎつつ、コンポーネント単位で段階的に OnPush へ移行できる。

### リアクティブ開発のための新ツール

- **`@Service()` デコレータ**: root スコープへの自動提供をボイラープレートなしで実現（`autoProvided: false` でカスタム登録）
- **`injectAsync()`**: サービスのオンデマンドロード。`onIdle()` と連携してブラウザアイドル時にプリフェッチ

### Router / テンプレート構文の改善

- `isActive()` が Signal を返し、ルートのアクティブ状態をリアクティブに参照可能
- ワイルドカードが前後セグメント付きパターン（`foo/**/bar`）をサポート
- テンプレートでオブジェクト/配列スプレッド・rest・アロー関数（暗黙 return）・`instanceof`・網羅的 `@switch`（`@default never`）をサポート
- オプショナルチェイニング `?.` を JavaScript セマンティクスに準拠するよう修正

### インフラ更新

- **FetchBackend がデフォルト**: `XMLHttpRequest` を置き換え。アップロード進捗が必要な場合は明示的に `withXhr()`
- **Incremental Hydration がデフォルト有効**: 無効化は `withNoIncrementalHydration()`
- **Shadow DOM**: shadow root 内での bootstrap をサポート
- **TypeScript 6 対応**（5.9 は deprecated）、**Node.js 26 互換**

## 破壊的変更・移行ガイド

- **OnPush デフォルト化**: `ng update` が `Eager` を自動付与するため即時の挙動変化はなし。移行はコンポーネント単位で段階的に。
- **FetchBackend デフォルト化**: アップロード進捗イベントに依存している場合は `withXhr()` を明示。
- **TypeScript 5.9 の deprecate**: TS 6 への更新を計画する。
- 自動ハイドレーションで問題が出る場合は `withNoIncrementalHydration()` で一時的に無効化可能。

## 今後の注目点

- Signal Forms / Resource API の安定化により、Reactive Forms からの移行ガイドとエコシステム対応（フォームライブラリ等）の追従が進むか。
- OnPush デフォルト化を機に、Zoneless 構成への移行がさらに後押しされる見込み。
- AI ツーリング（Angular の AI 連携機能）の今後の拡充。
