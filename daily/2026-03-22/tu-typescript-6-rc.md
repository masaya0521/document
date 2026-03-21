# TypeScript 6.0 RC — JS コードベース最後のリリースと Go ベース TS7 への道

- **日付**: 2026-03-06
- **カテゴリ**: Language
- **ソース**: [TypeScript DevBlogs](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/03/06/typescript-6-0-rc-bridges-to-go-based-future.aspx)

## 概要

TypeScript 6.0 RC は、現在の JavaScript コードベースに基づく最後のメジャーリリースとなる移行版。次の TypeScript 7.0 は Go 言語で書き直されたネイティブコンパイラを採用し、ネイティブコード速度と共有メモリマルチスレッドによる大幅なパフォーマンス向上が見込まれている。6.0 では多くのデフォルト値が変更され、非推奨オプションの廃止が進められており、7.0 へのスムーズな移行を意図した設計になっている。

## 主な変更点

### 新機能
- **`this` を使わない関数の型推論改善**: メソッド構文でもアロー関数と同様の推論が機能
- **サブパスインポート `#/` サポート**: `"#": "./dist/index.js"` のようなシンプルなマッピングが可能に
- **`--stableTypeOrdering` フラグ**: 型 ID の割り当てを宣言順序に依存しない方式に変更可能（TS7 移行時の差分削減用）
- **Temporal API 対応**: ECMAScript Temporal 提案（Stage 3）の型定義を組み込み
- **`RegExp.escape()`**: 正規表現の特殊文字を自動エスケープする関数の型定義
- **Map/WeakMap の `upsert` メソッド**: `getOrInsert` と `getOrInsertComputed` を追加

### デフォルト値の重要な変更

| オプション | 旧デフォルト | 新デフォルト |
|----------|-----------|-----------|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | `es2020` | `es2025` |
| `types` | すべて自動列挙 | `[]`（空配列） |
| `rootDir` | 推論 | `.`（tsconfig.json のディレクトリ） |

## 破壊的変更・移行ガイド

### 即座に対応が必要な項目

1. **`types` フィールドの明示的設定**: Node.js 環境では `"types": ["node"]` を指定しないと `Cannot find module` エラーが大量発生する
2. **`rootDir` の明示的設定**: ソースファイルが tsconfig.json より深い階層にある場合は `"rootDir": "./src"` を設定
3. **`strict: true` がデフォルト**: 明示的に `false` を設定していない場合、strict モードが有効化される

### TypeScript 7.0 で完全削除予定のオプション

6.0 では非推奨警告が出るが、`"ignoreDeprecations": "6.0"` で抑制可能。7.0 で完全削除。

- `target: es5`
- `--downlevelIteration`
- `--moduleResolution node`（node10）
- `--module amd/umd/systemjs/none`
- `--baseUrl`（パスエイリアス用途は `paths` で代替）
- `--moduleResolution classic`
- `esModuleInterop: false`
- `allowSyntheticDefaultImports: false`
- `--outFile`
- import assertions（`asserts` → `with` に変更）

### 推奨マイグレーション手順

1. TypeScript 6.0 RC にアップグレード（`npm install -D typescript@rc`）
2. `tsconfig.json` で `types` と `rootDir` を明示的に設定
3. 非推奨警告をすべて解消
4. `--stableTypeOrdering` を有効化して出力の安定性を確認
5. 準備ができたら TypeScript 7.0 に移行

## 今後の注目点

- TypeScript 7.0（Go ベース）のリリース時期
- Go ベースコンパイラでの型チェック並列化による実際のパフォーマンス向上幅
- エディタ / IDE の Language Service の Go ベース版への移行状況
- エコシステム（ESLint, Prettier 等）の TS7 対応状況
