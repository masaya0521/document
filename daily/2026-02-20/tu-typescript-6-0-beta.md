# TypeScript 6.0 Beta — JS ベース最後のリリースと 7.0 への移行準備

- **日付**: 2026-02-20
- **カテゴリ**: Language
- **ソース**: [公式アナウンス](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/), [GitHub Releases](https://github.com/microsoft/typescript/releases)

## 概要

TypeScript 6.0 Beta は 2026 年 2 月 11 日に公開された。現在の JavaScript コードベースに基づく最後のメジャーリリースとなり、Go 言語で書き直される TypeScript 7.0 への移行を円滑にすることが主目的。デフォルト値の大幅変更（`strict: true`、`target: es2025` 等）や多数のレガシーオプションの非推奨化が含まれ、既存プロジェクトへの影響が大きい。RC は 2 月 24 日、正式リリースは 3 月 17 日予定。

## 主な変更点

### 新機能

#### ES2025 / Temporal API サポート

`target` と `lib` に `ES2025` が追加され、以下の新しい API の型定義が利用可能になった。

- **`RegExp.escape`**: 正規表現の特殊文字を自動エスケープ
- **Temporal API**: 日時処理の新しい標準 API（Stage 3）
- **Map/WeakMap の upsert メソッド**: `getOrInsert`、`getOrInsertComputed`

#### `this` なし関数のコンテキスト感度低減

メソッド構文で定義されていても、`this` が実際に使用されていない関数はコンテキスト的に敏感でないと判定されるようになり、型推論が改善される。

#### サブパスインポートで `#/` をサポート

Node.js の最新仕様に対応し、`package.json` の `imports` フィールドで `#/` プレフィックスが利用可能に。

#### DOM ライブラリの統合

`lib.dom.iterable` と `lib.dom.asynciterable` が `lib.dom` に統合。個別のインクルードが不要になった。

#### `--stableTypeOrdering` フラグ

TypeScript 7.0（Go ベース）との型順序の一貫性を確保するためのフラグ。有効にするとパフォーマンスが最大 25% 低下するが、7.0 への移行テストに有用。

#### `--moduleResolution bundler` と `--module commonjs` の組み合わせ

以前は `esnext` / `preserve` のみだったが、`commonjs` とも組み合わせ可能になった。

## 破壊的変更・移行ガイド

### デフォルト値の変更

| オプション | 旧デフォルト | 新デフォルト |
|-----------|------------|------------|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | `es2020` | `es2025` |
| `types` | 全ての `@types` | `[]`（空配列） |
| `rootDir` | 推論 | `.`（tsconfig.json 所在地） |

### 非推奨化されるオプション（7.0 で完全削除予定）

以下のオプションは `"ignoreDeprecations": "6.0"` を設定することで一時的に継続利用可能。

- `--target es5`
- `--moduleResolution node`（node10）
- `--moduleResolution classic`
- `--module amd/umd/systemjs`
- `--baseUrl`（パスエイリアス用途は `paths` に移行）
- `--outFile`
- `--downlevelIteration`
- `--esModuleInterop false`
- `--allowSyntheticDefaultImports false`
- `--alwaysStrict false`
- 従来の `module` キーワード（namespace に統一）
- インポート `asserts` 構文（`with` に統一）

### 推奨される移行手順

**1. `types` フィールドの明示的設定**

```json
{
  "compilerOptions": {
    "types": ["node", "jest"]
  }
}
```

新デフォルトでは `@types` パッケージが一切読み込まれないため、明示的な指定が必須。

**2. `rootDir` の明示化**

```json
{
  "compilerOptions": {
    "rootDir": "./src"
  }
}
```

**3. `baseUrl` から `paths` への移行**

```json
{
  "compilerOptions": {
    "paths": {
      "@app/*": ["./src/app/*"],
      "@lib/*": ["./src/lib/*"]
    }
  }
}
```

**4. 段階的な移行フロー**

1. TypeScript 6.0 にアップグレード
2. 非推奨警告を解決
3. 必要に応じて明示的な型注釈を追加
4. `--stableTypeOrdering` で 7.0 との差分を確認
5. TypeScript 7.0 リリース後に移行

## 今後の注目点

- **TypeScript 6.0 RC**: 2026 年 2 月 24 日
- **TypeScript 6.0 正式リリース**: 2026 年 3 月 17 日
- **TypeScript 7.0（Go ベース）**: 6.0 直後にリリース予定。ネイティブプレビューは `@typescript/native-preview`（npm）で利用可能
- 7.0 では上記の非推奨オプションが完全削除され、ビルド速度が最大 10 倍向上する見込み
- TypeScript 7.0 の VS Code 拡張機能も既に提供中
