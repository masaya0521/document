# TypeScript 6.0 — Go ネイティブ 7.0 への橋渡しリリース

- **日付**: 2026-03-23
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [GitHub Releases](https://github.com/microsoft/typescript/releases)

## 概要

TypeScript 6.0 は JavaScript ベースのコンパイラとしては最後のメジャーリリースとなる歴史的なバージョンである。数ヶ月以内にリリース予定の TypeScript 7.0（Go によるフルリライト）への橋渡しを主目的とし、デフォルト設定の大幅な変更と多数のレガシーオプションの廃止を含む。

新機能としては `es2025` ターゲット、Temporal API の型定義、`#/` サブパスインポート対応などが追加されている。インクリメンタルコンパイルが 40-60% 高速化、メモリ使用量が 25% 削減されるなど、パフォーマンス面でも改善がある。

## 主な変更点

### デフォルト設定の変更

9つのデフォルト設定が一括で変更された。影響の大きいものは以下の通り。

| 設定項目 | 旧デフォルト | 新デフォルト |
|---------|-----------|-----------|
| `strict` | `false` | `true` |
| `module` | （推論） | `esnext` |
| `target` | `es2020` | `es2025` |
| `types` | すべての `@types` | `[]`（明示指定が必要） |
| `rootDir` | 推論 | `.`（tsconfig.json のディレクトリ） |

### 新しい言語機能

- **Temporal API 型定義**: Stage 4 に到達した時間処理 API（`Temporal.PlainDate`, `Temporal.ZonedDateTime` 等）
- **`#/` サブパスインポート**: Node.js 20 対応の `package.json` `imports` フィールド
- **`Map.getOrInsert` / `getOrInsertComputed`**: Map の upsert 操作
- **`RegExp.escape()`**: 正規表現文字列のエスケープ
- **`this` 非使用メソッドの型推論改善**: コールバック渡し時の型推論精度向上

### パフォーマンス改善

- インクリメンタルコンパイル: 40-60% 高速化
- メモリ使用量: 25% 削減
- エディタ操作: 30% 高速化

## 破壊的変更・移行ガイド

### 削除されたオプション

以下のオプションは TypeScript 6.0 で完全に削除された。

- `--target es5`（最低ターゲットは `ES2015`）
- `--downlevelIteration`
- `--moduleResolution node`（node10）/ `classic`
- `--module amd` / `umd` / `systemjs` / `none`
- `--outFile`
- `--esModuleInterop false`

### 廃止された構文

- `module Foo { ... }` → `namespace Foo { ... }` を使用
- `import asserts { ... }` → `import with { ... }` に変更

### 移行手順

1. **即座に対応が必要な設定の明示化**:
   ```json
   {
     "compilerOptions": {
       "types": ["node"],
       "rootDir": "./src"
     }
   }
   ```

2. **段階的な廃止対応**: `"ignoreDeprecations": "6.0"` を設定すれば、廃止警告を一時的に抑制可能

3. **7.0 への準備**: `--stableTypeOrdering` フラグを有効にすると、型の順序が 7.0 と一致するようになる（最大 25% の速度低下あり）

## 今後の注目点

- **TypeScript 7.0**: Go ネイティブコンパイラとして数ヶ月以内にリリース予定。10.8x のコンパイル高速化、30x の型チェック高速化、2.9x のメモリ削減が報告されている
- **tsgo**: TypeScript 7.0 のネイティブプレビュー版が npm と VS Code 拡張で既に利用可能
- **エコシステム影響**: ES5 ターゲット廃止により、レガシーブラウザサポートが必要なプロジェクトは別途トランスパイラが必要
