# Angular — v22.0 リリース

- **日付**: 2026-06-03（採録日: 2026-06-16）
- **カテゴリ**: Frontend
- **ソース**: [Ninja Squad: What's new in Angular 22.0](https://blog.ninja-squad.com/2026/06/03/what-is-new-angular-22.0), [Angular.love: Angular 22 Key Features](https://angular.love/angular-22-key-features-and-changes), [ANGULARarchitects](https://www.angulararchitects.io/en/blog/angular-22-the-most-important-new-features-at-a-glance/)

## 概要

Angular 22 は 2026 年 6 月 3 日にリリースされ、これまで実験的・段階的に導入されてきた **Signal ベースのリアクティビティ** を一気に「production-stable」へ引き上げたメジャーリリースである。Signal Forms と各種 Resources が安定化し、変更検知のデフォルトが `OnPush` に、HttpClient のデフォルトが Fetch API になるなど、「signal-first（シグナル優先）時代」を象徴する既定値の変更が多数含まれる。

半年ごとのリリースサイクルに沿った定期メジャーであり、Angular 21（2025 年 11 月）で developer preview / experimental だった機能群がまとめて卒業した形になる。

## 主な変更点

### Signal Forms / Resources の安定化

- **Signal Forms** が experimental から正式版へ。`minDate()` / `maxDate()` バリデータ、blur 時のデバウンス、特定のバリデーションエラーへアクセスする `getError()` メソッドなどを追加。
- **Resources**（`resource()` / `rxResource()` / `httpResource()`）も安定化。`chain()` メソッドによるチェーンが改善。

### 変更検知のデフォルトが OnPush に

- 新規コンポーネントの既定の変更検知戦略が `Eager` から **`OnPush`** に変更。
- 既存挙動を保つため、自動マイグレーションが既存コンポーネントに `changeDetection: ChangeDetectionStrategy.Eager` を明示的に付与する。

### HttpClient が Fetch API デフォルトに

- HttpClient のデフォルト実装が `XMLHttpRequest` から **Fetch API** へ。
- `withFetch()` オプションは非推奨に。`reportProgress` は `reportUploadProgress` / `reportDownloadProgress` に分割。

### DI / 遅延ロードの改善

- **`@Service` デコレータ** を新設。`@Injectable({ providedIn: 'root' })` のより簡潔な代替で、`inject()` による DI を前提とする root 提供サービスを宣言できる。
- **`injectAsync()`** により、動的 import でサービスをオンデマンドに遅延ロード可能。`onIdle` などの prefetch 戦略も指定できる。

### その他

- `strictTemplates` がデフォルト有効化。
- `@defer` ブロックが idle timeout をサポート。
- SSR の **Incremental Hydration がデフォルト** に。
- **Angular ARIA** パッケージが GA に。
- AI 連携向けの実験的 WebMCP ツールを追加。
- selectorless components（文字列セレクタなしでテンプレートに直接 import）の開発が継続。

## 破壊的変更・移行ガイド

- **必須環境のアップグレード**: TypeScript v6 / Node.js v22 が必須に。
- `markAsTouched()` がデフォルトで子孫要素も touched としてマークするように変更。
- Router の `canMatch` 関数に必須の第 3 引数が追加。
- `paramsInheritanceStrategy` のデフォルトが `'always'` に変更（**自動マイグレーションは提供されない**ため手動確認が必要）。
- オプショナルチェーンのセマンティクスを TypeScript に合わせて調整。安全のため該当式は `$safeNavigationMigration()` でラップされる。

多くは `ng update` の自動マイグレーションでカバーされるが、`paramsInheritanceStrategy` の挙動変更と `OnPush` デフォルト化は実行時の動作差につながる可能性があるため、アップグレード後の回帰確認を推奨。

## 今後の注目点

- selectorless components の安定化に向けた進捗。大規模コードベースでの命名衝突低減・リファクタ容易性の向上が期待される。
- Signal Forms 安定化に伴う、従来の `ReactiveFormsModule` / `FormsModule` からの移行パスとエコシステム（フォームライブラリ）の追随。
- WebMCP など AI 連携ツールの発展。
