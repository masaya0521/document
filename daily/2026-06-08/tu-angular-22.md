# Angular — v22

- **日付**: 2026-06-08
- **カテゴリ**: Frontend
- **ソース**: [Angular v22 Release](https://angular.dev/events/v22), [What's new in Angular 22.0? — Ninja Squad](https://blog.ninja-squad.com/2026/06/03/what-is-new-angular-22.0), [Angular 22: The Most Important New Features — ANGULARarchitects](https://www.angulararchitects.io/en/blog/angular-22-the-most-important-new-features-at-a-glance/)

## 概要

Angular v22 が 2026年6月3日にリリースされた。過去2年かけて整備してきたリアクティブ API 群（Signal Forms、`resource()`、`httpResource`）が experimental を外れて安定化し、本番利用が可能になった点が最大のトピック。あわせて変更検知のデフォルトが OnPush に変わり、HttpClient が Fetch ベースになるなど、これまで「推奨設定」として手動で有効化していたものがフレームワークの既定値に格上げされた。Signal ベースのアーキテクチャへ全面的に舵を切る世代の到達点と言える。

## 主な変更点

### Signal API の安定化

- **Resource API**（`resource()` / `httpResource`）が stable に。非同期データ取得を Signal として宣言的に扱える。
- **Signal Forms** が stable に。フォームの状態を Signal で構成する新しいフォーム API。
- v21 で developer preview だった `@angular/aria`（アクセシビリティコンポーネント）も GA となり本番利用可。

### OnPush をデフォルト変更検知に

新規に生成されるコンポーネントは OnPush 変更検知をデフォルトで採用する。あわせて Router が全ての親ルートからルートパラメータを継承するようになった。

```typescript
// v22 では @Component に changeDetection を明示しなくても OnPush 相当の挙動が既定
@Component({
  selector: 'app-foo',
  template: `...`,
})
export class FooComponent {}
```

### HttpClient が Fetch ベースに

HTTP クライアントがデフォルトで Fetch API を使用する。`XMLHttpRequest` ベースから移行し、ストリーミングやキャンセルの扱いがモダンになる。

### `@Service` デコレータ（stable）

```typescript
@Service()
export class UserService {}
// 既定で @Injectable({ providedIn: 'root' }) と同等
// tree-shakeable なアプリケーション全体のシングルトンを、冗長な設定なしで宣言できる
```

### WebMCP 連携

WebMCP により、アプリケーションやフォームをブラウザ上で動作する AI エージェントが直接呼び出せる「ツール」として公開できるようになった。

### セキュリティ強化

SSRF（サーバサイドリクエストフォージェリ）対策を中心に多数の修正。`platform-server` で location/document 初期化を SSRF・パスハイジャックから保護、疑わしい URL の拒否、プロトコル相対 URL の制限、HttpClient のバックスラッシュ URL を介した SSRF バイパスの防止などを含む。

## 破壊的変更・移行ガイド

- **TypeScript 6 が必須**。v22 へ上げる前に TypeScript を 6 系へ更新する必要がある。
- **OnPush デフォルト化**: 既存の Default 変更検知前提のコンポーネントに依存している場合、新規生成物との混在に注意。`ng update` での移行が基本。
- **HttpClient の Fetch 化**: `XMLHttpRequest` 固有の挙動（progress イベントの細かい扱い等）に依存している箇所は要確認。
- 公式の `ng update @angular/core @angular/cli` で大半の移行は自動化される。

## 今後の注目点

- Signal Forms / Resource API が stable 化したことで、従来の `ReactiveFormsModule` ベースの実装からの移行ガイドやベストプラクティスが今後充実する見込み。
- WebMCP によるブラウザ内 AI エージェント連携は、フォームを「エージェントのツール」として扱う新しい UX パラダイムの起点になる可能性がある。
- OnPush デフォルト化により、Zoneless（Zone.js なし）構成への移行がさらに現実的になる。
