# TypeScript 6.0 Beta — Go リライトへの布石

- **日付**: 2026-02-27（リリース: 2026-02-11）
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/), [InfoQ](https://www.infoq.com/news/2026/02/typescript-6-released-beta/)

## 概要

TypeScript 6.0 Beta は、JavaScript ベースの TypeScript コンパイラとしては最後のリリースとなる。Go 言語で書き直される TypeScript 7.0 への移行をスムーズにするための「トランジションリリース」として位置づけられ、デフォルト設定の近代化、レガシー機能の非推奨化、ES2025 サポートが主な柱となっている。7.0 では非推奨オプションが完全削除されるため、6.0 の段階で対応を済ませておくことが強く推奨されている。

## 主な変更点

### デフォルト設定の変更

6.0 で多くのデフォルト値が変更された。既存プロジェクトへの影響が大きいため注意が必要。

| 設定 | 旧デフォルト | 新デフォルト |
|---|---|---|
| `strict` | `false` | **`true`** |
| `module` | `commonjs` | **`esnext`** |
| `target` | `es2020` | **`es2025`** |
| `rootDir` | 自動推論 | **tsconfig.json のディレクトリ** |
| `types` | 全て列挙 | **`[]`（空配列）** |

### 新機能

- **`this` 未使用関数の文脈感度低減**: `this` を使用しない関数で、メソッド構文とアロー関数構文での型推論が一貫するように改善
- **`#/` サブパスインポート**: Node.js の最新サポートに対応し、`#/` プレフィックスでのサブパスインポートが可能に
- **`--moduleResolution bundler` と `--module commonjs` の組み合わせ**: 非推奨の `node` 解決戦略からの移行パスが拡大
- **`--stableTypeOrdering` フラグ**: 6.0 → 7.0 移行支援用。型の出力順序を安定化（最大 25% の性能低下の可能性あり）
- **ES2025 サポート**: `RegExp.escape`、Temporal API（Stage 3）、Map/WeakMap の `getOrInsert` メソッドなど
- **DOM lib 統合**: `lib.dom.d.ts` に `dom.iterable` と `dom.asynciterable` を統合

### 非推奨化される機能

以下の機能は 6.0 で非推奨となり、7.0 で完全削除される。`"ignoreDeprecations": "6.0"` で一時的に警告を抑制可能。

- `target: es5`
- `--downlevelIteration`
- `--moduleResolution node`（node10）/ `classic`
- `--module amd` / `umd` / `systemjs`
- `--baseUrl`（パス解決としての機能）
- `--outFile`（バンドル出力）
- `esModuleInterop: false` / `allowSyntheticDefaultImports: false`
- `namespace` の代わりの `module` キーワード
- import assertions（`asserts` → `with` への移行）

## 破壊的変更・移行ガイド

### 1. `types` 設定の明示化

デフォルトが空配列になったため、`@types/node` など必要な型定義を明示的に指定する必要がある。

```json
{
  "compilerOptions": {
    "types": ["node"]
  }
}
```

### 2. `rootDir` の明示化

自動推論が廃止されたため、明示的に指定する。

```json
{
  "compilerOptions": {
    "rootDir": "./src"
  }
}
```

### 3. `baseUrl` からの移行

`baseUrl` がパス解決として機能しなくなるため、`paths` に直接パスを記述する形式に変更する。

```json
// Before
{
  "compilerOptions": {
    "baseUrl": "./src",
    "paths": { "@app/*": ["app/*"] }
  }
}

// After
{
  "compilerOptions": {
    "paths": { "@app/*": ["./src/app/*"] }
  }
}
```

### 4. 段階的な移行戦略

1. まず TypeScript 6.0 Beta をインストール
2. `"ignoreDeprecations": "6.0"` を設定して既存コードをコンパイル
3. 非推奨警告を一つずつ解消
4. 7.0 リリース前に全ての非推奨機能を置き換え

## 今後の注目点

- **TypeScript 7.0**: Go ベースのコンパイラ（コードネーム "Corsa"）として 6.0 直後にリリース予定。コンパイル速度 5〜10 倍、エディタ起動 8 倍高速化、メモリ使用量 50% 削減が目標
- 6.0 → 7.0 間の互換性検証ツールとして `--stableTypeOrdering` が提供されているため、早期に有効化してテストすることを推奨
- ネイティブプレビュー版が npm で公開中のため、7.0 の動作確認も並行して可能
