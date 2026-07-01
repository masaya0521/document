# Angular — 22.0

- **日付**: 2026-06-03
- **カテゴリ**: Frontend
- **ソース**: [What's new in Angular 22.0? — Ninja Squad](https://blog.ninja-squad.com/2026/06/03/what-is-new-angular-22.0), [Angular v22 Release](https://angular.dev/events/v22), [ANGULARarchitects](https://www.angulararchitects.io/en/blog/angular-22-the-most-important-new-features-at-a-glance/)

## 概要

Angular 22 は、単一の目玉機能ではなく「3年かけた signals・アクセシビリティ・リアクティブアーキテクチャへの投資がロードマップから日常の標準に変わる」節目のリリース。**Signal Forms・Resource API・Angular Aria の安定化**、変更検出のデフォルト **OnPush 化**、HttpClient の **Fetch API デフォルト化** が並ぶ。

環境要件が引き上げられており、**TypeScript v6 が必須**（v5.9 以下は非対応）、**Node は v22** をサポート（v20 は非対応）。

## 主な変更点

### Signal Forms の安定化
実験段階から本番利用可能へ昇格。FormGroup/FormControl の複雑な構成に頼らず、Signals でフォーム値・バリデーション状態・送信を管理する。

- `touched` 入力でフィールド状態を確認、`touch()` 出力でマークする形に整理。
- `markAsTouched()` はフィールドと全子孫をマーク（`skipDescendants: true` で制御可能）。
- `minDate()` / `maxDate()` バリデータを追加。
- 非同期バリデータのデバウンス対応。

```typescript
validateHttp(field, { debounce: 400 })
```

### 変更検出のデフォルトが OnPush に
明示指定のないコンポーネントは従来の Eager ではなく **OnPush** を採用。自動マイグレーションが提供され後方互換を維持。

### Resource API の安定化
`resource()` / `rxResource()` / `httpResource()` が本番対応に。`chain()` メソッドで依存リソースの管理が容易化。

### HttpClient の Fetch API デフォルト化
XMLHttpRequest から Fetch へ移行。既存の HttpClient API は変更なしで互換維持。ただしアップロード進捗系の一部挙動が変わる（`reportUploadProgress` / `reportDownloadProgress` を利用）。

### 新デコレータ `@Service()`
`@Injectable({ providedIn: 'root' })` の簡潔な糖衣構文。

```typescript
@Service()
class UserService {}
```

### `injectAsync()`
遅延読み込みサービスを動的インポートで注入。

```typescript
private readonly reportService = injectAsync(() => import('./report.service'));
```

### テンプレートの改善
- `strictTemplates` がデフォルト有効化。
- 要素内コメント `<div /* comment */>` に対応。
- オプショナルチェーンの挙動改善（`@if (project?.author) { {{ project.author }} }` が正常動作）。

### Angular Aria の安定化
`@angular/aria` パッケージがアクセシブルな UI パターン、カスタマイズ可能なスタイリング、Signal Forms 連携、テストハーネスを提供。キーボード・マウス・スクリーンリーダー等に対応。

## 破壊的変更・移行ガイド

| 項目 | 対応方法 |
|------|--------|
| `strictTemplates` デフォルト有効化 | テンプレート型エラーの解消が必要な場合あり |
| 変更検出が OnPush デフォルト | 自動マイグレーション提供。手動 `markForCheck` が必要な箇所を確認 |
| `paramsInheritanceStrategy` デフォルト | 従来動作維持には明示的に `'emptyOnly'` 指定 |
| `canMatch` 関数の第3引数 | 必須化（自動マイグレーション対応） |
| TypeScript 要件 | v6 必須（v5.9 以下は非対応）。先に TS 側を更新 |
| Node 要件 | v22 サポート（v20 非対応） |

## 今後の注目点

- AI ツール連携: Google AI Studio / Gemini Canvas から Angular アプリを生成・反復できる方向。WebMCP 実装（`declareExperimentalWebMcpTool()`）でエージェント統合も。
- Signal Forms・Resource の安定化で「signals ファースト」な設計が実務標準に。既存の Reactive Forms からの段階的移行方針を検討する時期。
- TypeScript 6 必須化により、TS 7.0（Go ネイティブコンパイラ）への移行と歩調を合わせやすくなる。
