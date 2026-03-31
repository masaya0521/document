# TypeScript 6.0 — JavaScript ベース最後のメジャーリリース

- **日付**: 2026-03-23
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [GitHub Releases](https://github.com/microsoft/typescript/releases)

## 概要

TypeScript 6.0 は、現行の JavaScript ベースコンパイラとしては最後のメジャーリリースとなる。Go 言語で書き直される TypeScript 7.0 への橋渡しとして、デフォルト設定の近代化と非推奨オプションの整理に重点が置かれている。新機能としては Temporal API の型サポート、`this` を使わない関数のコンテキスト感度改善、サブパスインポートの `#/` 構文対応などが含まれる。

## 主な変更点

### デフォルト値の近代化

最も影響範囲の大きい変更は、コンパイラオプションのデフォルト値の刷新:

| オプション | 旧デフォルト | 新デフォルト |
|----------|----------|-----------|
| `strict` | `false` | **`true`** |
| `module` | `commonjs` | **`esnext`** |
| `target` | `es2020` | **`es2025`** |
| `types` | 全 `@types/*` 自動包含 | **`[]`（空）** |
| `rootDir` | 推測 | **`.`** |

特に `types: []` への変更は多くのプロジェクトに影響する。従来は `@types/*` パッケージが自動的にグローバルスコープに含まれていたが、6.0 からは明示的な指定が必要:

```json
{
  "compilerOptions": {
    "types": ["node", "jest"]
  }
}
```

### 新しい組み込み API 型

Stage 4 に到達した **Temporal API** の型定義が組み込みで利用可能に:

```typescript
let yesterday = Temporal.Now.instant().subtract({ hours: 24 });
```

その他:
- `Map.prototype.getOrInsert` / `getOrInsertComputed`
- `RegExp.escape`

### `this` を使わない関数のコンテキスト感度改善

メソッド構文で `this` を使用しない関数は、コンテキスト依存関数として扱われなくなり、ジェネリック呼び出しでの型推論が改善:

```typescript
callIt({
    consume(y) { return y.toFixed(); },
    produce(x: number) { return x * 2; },
});
```

### サブパスインポート `#/` 構文

Node.js の `imports` フィールドに対応する `#/*` 構文をサポート:

```json
{
  "imports": {
    "#/*": "./dist/*"
  }
}
```

### `--stableTypeOrdering` フラグ

TypeScript 6.0 と 7.0 間での型順序の違いを検出する診断用フラグ。パフォーマンスが最大 25% 低下するため、CI での検証用途に限定して使用を推奨。

## 破壊的変更・移行ガイド

### 非推奨となるオプション

| 廃止対象 | 理由 |
|--------|------|
| `--target es5` | レガシー環境の利用が希少に |
| `--moduleResolution node` | 古い Node.js 10 仕様 |
| `--module amd/umd/systemjs` | ESM が標準化 |
| `--baseUrl` | パス指定で置換可能 |
| `--outFile` | 外部バンドラーに統合 |
| legacy `module` 構文 | `namespace` キーワードに統合 |

### 移行手順

1. `tsconfig.json` に `"types"` フィールドを明示的に追加（グローバル型が必要な場合）
2. `strict: true` がデフォルトになるため、既に `strict: true` を設定しているプロジェクトは影響なし
3. `module: "commonjs"` を使っているプロジェクトは明示的に指定するか、ESM への移行を検討
4. `--stableTypeOrdering` フラグで 7.0 との互換性を事前に確認

## 今後の注目点

- **TypeScript 7.0**: Go 言語で書き直されたネイティブコンパイラ。共有メモリマルチスレッディングにより大幅な高速化が見込まれる。数ヶ月以内にリリース予定
- ネイティブプレビュー版が既に利用可能（`npx @typescript/native`）
- 6.0 で `--stableTypeOrdering` を使い、7.0 との型互換性を事前に検証しておくことを推奨
