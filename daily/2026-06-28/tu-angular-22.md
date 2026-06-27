# Angular 22 — signal-first 時代への移行

- **日付**: 2026-06-28
- **カテゴリ**: Frontend
- **ソース**: [Announcing Angular v22 (Angular Blog)](https://blog.angular.dev/announcing-angular-v22-c52bb83a4664), [Angular 22: The Most Important New Features at a Glance (ANGULARarchitects)](https://www.angulararchitects.io/en/blog/angular-22-the-most-important-new-features-at-a-glance/)

## 概要

Angular 22 が 2026年6月3日にリリースされ（最新パッチは 6月17日の v22.0.2）、フレームワークは本格的に "signal-first" 時代へ移行した。これまで experimental 扱いだった Signal Forms、Resource API、非同期リアクティビティ API が production-ready の安定版に昇格し、Signal を中心とした宣言的なデータフローが標準的な書き方として確立された。

加えて、変更検知のデフォルトが `Default` から `OnPush` に切り替わるという、長年の Angular にとって大きな転換点となる変更が含まれている。新規プロジェクトはより高速な変更検知をデフォルトで享受でき、既存プロジェクトは `ng update` による互換性維持の仕組みで段階的に移行できる。

## 主な変更点

### Signal Forms / Resource API の安定化

- **Signal Forms**: Reactive Forms の堅牢さ・強い型付け、Template-driven Forms の手軽さ、そして Signal のリアクティビティを統合した新しいフォーム API。experimental から安定版へ昇格。
- **Resource API**: Signal エコシステムにおける「非同期データ取得の欠けたピース」だった部分が埋まった。`resource`、`rxResource`、`httpResource` が安定版となり、リアクティブな HTTP リクエスト・派生データを宣言的に扱える。

### `@Service` デコレータ

```ts
// Before
@Injectable({ providedIn: 'root' })
export class UserService {}

// After
@Service()
export class UserService {}
```

`@Injectable()` や `@Injectable({ providedIn: 'root' })` の典型的なケースを置き換える、より簡潔な新デコレータ。

### `injectAsync` による遅延ロード

ラムダ式が返す Promise を受け取り、サービスをオンデマンドで読み込む。`onIdle` によるプリフェッチに対応し、ユーザー体感の遅延を最小化する。

### `debounced` 関数

指定した遅延で値が更新される Resource を生成する。純粋な Signal チェーンではこれまで扱いにくかった時間ベースのリアクティビティ（デバウンス）に対応。

### テンプレート / Router の強化

- テンプレート構文に object/array のスプレッド演算子、アロー関数、`instanceof` チェックを追加
- `@switch` の網羅性チェック（`@default never;` による exhaustive validation）
- Router に `isActive` Signal 関数が追加され、ルートのアクティブ状態をリアクティブに検出可能

## 破壊的変更・移行ガイド

- **`OnPush` がデフォルトの変更検知戦略に**: 既存コンポーネントの挙動を壊さないよう、`ng update` は明示的な戦略を持たないコンポーネントに対して自動で `ChangeDetectionStrategy.Eager` を適用する。これにより従来の `Default` 相当の挙動が維持されるため、アップグレード直後に挙動が変わることはない。新規コンポーネントから `OnPush` を前提とした設計に寄せていくのが推奨。
- **`FetchBackend` がデフォルトに**: `HttpClient` のバックエンドが Fetch ベースに。これに伴い `reportProgress` が `reportDownloadProgress` と `reportUploadProgress` に分割された。アップロード進捗を取得する場合は明示的に `withXhr()` の設定が必要。

## 今後の注目点

- Signal Forms の本格採用により、Reactive Forms / Template-driven Forms との使い分け・移行のベストプラクティスがコミュニティで固まっていくか
- `OnPush` デフォルト化を機に、Zone.js レス（zoneless）構成への移行がさらに進むか
- Resource API と SSR / ハイドレーションの組み合わせにおける実運用パターンの蓄積
