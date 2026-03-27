# TypeScript 6.0 — JavaScript ベース最終リリースと Go 移行への道

- **日付**: 2026-03-23
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/03/23/typescript-6-0-ships-as-final-javascript-based-release-clears-path-for-go-native-7-0.aspx)

## 概要

TypeScript 6.0 は、JavaScript で書かれた TypeScript コンパイラの最終メジャーリリースである。次期 TypeScript 7.0 は Go 言語で完全に再実装される（コードネーム "Corsa"）予定で、6.0 はそこへの橋渡しとして位置づけられている。9つのデフォルト設定の一斉変更と多数の非推奨化が含まれており、既存プロジェクトの移行準備が主な目的のリリースとなっている。

## 主な変更点

### 新機能

- **ES2025 サポート**: 新しい `target` と `lib` オプションで ES2025 を指定可能
- **Temporal API 型定義**: Stage 4 に到達した Temporal API の型定義を追加
- **サブパスインポート (`#/`) 対応**: Node.js 20 で追加された `#/*` パターンをサポート
- **`this` を使用しない関数の型推論改善**: メソッド構文でも `this` を使わなければアロー関数同様に型推論が機能
- **`--stableTypeOrdering` フラグ**: 6.0 から 7.0 への移行時に型順序の安定性を確保

### デフォルト値の変更（9項目）

| 設定項目 | 旧デフォルト | 新デフォルト | 影響 |
|---------|-----------|-----------|------|
| `strict` | `false` | `true` | より厳密な型チェック |
| `module` | `commonjs` | `esnext` | ESM 中心へ |
| `target` | `es2020` | `es2025` | 最新 JS 対応 |
| `types` | 全 `@types/*` を自動検出 | `[]`（空配列） | ビルド時間 20-50% 短縮 |
| `rootDir` | 推論 | `.`（tsconfig.json の位置） | 明示指定が必要な場合あり |
| `esModuleInterop` | `false` | 常に `true`（設定不可） | — |
| `allowSyntheticDefaultImports` | `false` | 常に `true`（設定不可） | — |
| `alwaysStrict` | `false` | 常に `true`（設定不可） | — |

特に影響が大きいのは `types` のデフォルト変更で、`@types/node` や `@types/jest` 等を使っている場合は明示的に指定が必要になる：

```json
{
  "compilerOptions": {
    "types": ["node", "jest"]
  }
}
```

### 削除されたオプション

- `target: es5` — ES2015 以上が必須に
- `--moduleResolution node`（node10）— `nodenext` または `bundler` へ移行
- `--module amd/umd/systemjs/none` — ESM への統一
- `--baseUrl` — `paths` に統合
- `--outFile` — 外部バンドラー利用を推奨
- `import assertions`（`asserts`）— `with` 構文に変更

## 破壊的変更・移行ガイド

### 最初に確認すべき項目

多くのプロジェクトで以下のいずれかが必要：

1. `"types": ["node"]` を明示的に指定
2. `"rootDir": "./src"` を設定（以前の推論に依存していた場合）

### `baseUrl` からの移行

```json
// Before
{
  "baseUrl": "./src",
  "paths": { "@app/*": ["app/*"] }
}

// After
{
  "paths": { "@app/*": ["./src/app/*"] }
}
```

### 移行ツール

- **`ts5to6` ツール**: `baseUrl` や `rootDir` の自動調整に対応
- **`"ignoreDeprecations": "6.0"`**: tsconfig に指定することで非推奨警告を一時的に抑制可能（7.0 では廃止）

## 今後の注目点

- **TypeScript 7.0（Corsa）**: Go 言語での完全再実装。数ヶ月以内のリリース見込み
  - コンパイル速度 5-10 倍向上
  - エディタ起動時間 約8倍改善
  - メモリ使用量 約50% 削減
  - 共有メモリ・マルチスレッドによる並列型チェック
- **プレビュー試用**: `@typescript/native-preview` パッケージで 7.0 を先行試用可能
- **6.0 の `ignoreDeprecations` は 7.0 で完全廃止** — 6.0 期間中に非推奨オプションの移行を完了する必要がある
