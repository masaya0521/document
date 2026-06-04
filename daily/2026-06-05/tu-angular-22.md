# Angular — v22.0 リリース

- **日付**: 2026-06-05（リリース日: 2026-06-03）
- **カテゴリ**: Frontend
- **ソース**: [Ninja Squad — What's new in Angular 22.0](https://blog.ninja-squad.com/2026/06/03/what-is-new-angular-22.0), [Angular v22 Release（angular.dev）](https://angular.dev/events/v22), [Versioning and releases](https://angular.dev/reference/releases)

## 概要

Angular 22 が 2026年6月3日にリリースされた。これまで実験的・開発者プレビューだった **Signal Forms**・**Resource API**・**Angular Aria** が一斉に安定化し、コミュニティが「signal-first era（シグナルファースト時代）」と呼ぶ節目となるメジャーリリース。

同時にフレームワークのデフォルト設定がモダン化され、`OnPush` 変更検知・Fetch ベースの HttpClient・`strictTemplates` がデフォルトになった。さらに **TypeScript 6 が必須**となり、Node 20 のサポートが打ち切られるなど、アップグレード時に対応が必要な破壊的変更も多い。

## 主な変更点

### 安定化した主要 API

- **Signal Forms** が experimental から production-ready へ
  - `minDate()` / `maxDate()` バリデータを追加
  - blur 時の `debounce` オプション、エラー取得を簡潔にする `getError()` を追加
- **Resources**（`resource()` / `rxResource()` / `httpResource()`）が安定化
  - 依存管理用の `chain()` メソッド、`id` オプションによる SSR キャッシュ対応
- **`@angular/aria`** が開発者プレビューを卒業し、Signal Forms と連携した production-ready パッケージに

### デフォルトのモダン化

- コンポーネントの変更検知デフォルトが **`OnPush`** に
- HttpClient のデフォルトが **Fetch API**（XMLHttpRequest を置き換え）に
- **`strictTemplates`** がデフォルトで有効化

### 新しいデコレータ・関数

- **`@Service()`** — `@Injectable({ providedIn: 'root' })` のショートハンド
- **`injectAsync()`** — 遅延ロードされる依存の DI を可能にし、任意でプリフェッチも

### テスト・ツール

- **Karma → Vitest 移行** を `migrate-karma-to-vitest` スキーマティックで提供。Zone.js が Vitest と互換に
- AI 連携: `npx skills add` による Angular skills、`declareExperimentalWebMcpTool()` による WebMCP ツール宣言、Chrome DevTools の signal/injection グラフ統合
- SSR の **Incremental hydration がデフォルト**化（`withIncrementalHydration()` は非推奨に）

## 破壊的変更・移行ガイド

- **TypeScript v6 必須**: v5.9 以前は非サポート。先に TypeScript を上げる必要がある
- **Node v20 サポート終了**（Node v26 をサポート）
- **`withFetch()` / `reportProgress` が非推奨**: レガシー継続には `withXhr()`、進捗は `reportUploadProgress` / `reportDownloadProgress` を使用
- **Signal Forms の挙動変更**: `markAsTouched()` がデフォルトで子孫もマーク、`touched` が model から input/output パターンに変更
- **Router**: `canMatch` に第3引数 `currentSnapshot` が必須化
- 多くの修正は `ng update` 実行時の自動マイグレーションでカバーされるが、上記のランタイム挙動変更はコード側での確認が必要

### セキュリティ

- `platform-server` が SSRF・パスハイジャックを防御。疑わしい URL やプロトコル相対 URL を拒否し、HttpClient のバックスラッシュ URL 経由の SSRF バイパスを塞ぐ。多くは自動適用される

## 今後の注目点

- Signal Forms / Resource API の安定化により、RxJS 依存を減らしたシグナル中心の状態管理が標準アプローチになっていく
- WebMCP・Angular skills など AI エージェント向け統合の発展
- Vitest をデフォルトテストランナーに据える流れと、Karma 系プロジェクトの移行コスト
