# Angular — v22.0.0（signal-first 時代の到来）

- **日付**: 2026-06-19（リリースは 2026-06-03）
- **カテゴリ**: Frontend
- **ソース**: [Angular.love](https://angular.love/angular-22-key-features-and-changes), [ANGULARarchitects](https://www.angulararchitects.io/en/blog/angular-22-the-most-important-new-features-at-a-glance/), [DEV Community](https://dev.to/rigole/angular-22-is-here-everything-you-need-to-know-4g3c)

## 概要

Angular 22 は 2026年6月3日にリリースされた。Angular が「signal-first（シグナル優先）」へと舵を切るマイルストーンとなるバージョンで、これまで experimental だった主要 API が一斉に stable 化した。リアクティビティの中心がシグナルへ移り、変更検知のデフォルトも従来の `Default` から `OnPush` へと切り替わったことで、フレームワーク全体のパフォーマンス特性と書き味が大きく変化している。

加えて、ブラウザ上で動作する AI エージェントがアプリの機能を直接呼び出せる WebMCP 連携や、SSRF/パスハイジャック対策といったセキュリティ強化も盛り込まれた、実務インパクトの大きいメジャーリリースである。

## 主な変更点

### stable 化した API
- **Signal Forms**: シグナルベースのフォーム API が experimental を脱し、stable・サポート対象に。
- **`resource()` / `httpResource`**: 非同期データ取得をシグナルで扱う API が stable 化。宣言的な非同期リアクティビティを標準化。
- **Angular Aria**: アクセシビリティ向けの API が stable に。

### 変更検知のデフォルト変更
- **`OnPush` がデフォルトの変更検知戦略**に。不要な再評価を抑え、デフォルトでパフォーマンスの良い構成になる。
- ルーターは**親ルートすべてのルートパラメータをデフォルトで継承**するように変更。

### 新しい開発者向けビルディングブロック
- `@Service`、`injectAsync`、`debounced` といった、モダンでリアクティブなアプリ構築のためのより人間工学的な API を追加。

### AI 連携
- **WebMCP**: アプリやフォーム自体を、ブラウザ内で動作する AI エージェントが直接呼び出せる「ツール」として公開できる。

### セキュリティ強化
- `platform-server` が SSRF（サーバーサイドリクエストフォージェリ）とパスハイジャックをガード。
- 疑わしい URL・プロトコル相対 URL を拒否し、`HttpClient` のバックスラッシュ URL を経由した SSRF バイパスを塞ぐ。

## 破壊的変更・移行ガイド

- **`OnPush` デフォルト化**: 既存アプリで `Default` 戦略の暗黙的な再描画に依存していたコンポーネントは、`OnPush` 前提での挙動差に注意。`ChangeDetectorRef.markForCheck()` やシグナル経由での状態更新に揃える必要がある場合がある。
- **ルートパラメータ継承の変更**: 親ルートのパラメータがデフォルトで子に継承されるため、同名パラメータの解決順序や `ActivatedRoute` 経由の取得結果が変わる可能性がある。
- 安定化した API（Signal Forms / `resource()` / `httpResource`）は experimental 時代の暫定シグネチャから変更されている可能性があるため、プレビュー採用済みのコードは移行ガイドの確認を推奨。

## 今後の注目点

- signal-first への移行が進むことで、`NgModule` 〜 Standalone 〜 Signal という Angular の世代交代がさらに加速する見込み。
- WebMCP による「アプリ = AI エージェントのツール」というパラダイムが、フロントエンドの設計（フォーム・操作の宣言化）にどう波及するか。
- `resource()` / `httpResource` の stable 化により、RxJS への依存度がどこまで下がるか（共存か置き換えか）が実プロジェクトでの論点になる。
