# TypeScript 6.0 RC — Go ベース TypeScript 7.0 への橋渡し

- **日付**: 2026-03-11
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [InfoQ](https://www.infoq.com/news/2026/02/typescript-6-released-beta/), [InfoWorld](https://www.infoworld.com/article/4143186/typescript-6-0-reaches-release-candidate-stage.html)

## 概要

TypeScript 6.0 RC が 2026年3月6日にリリースされた。TypeScript 6.0 は **現在の JavaScript コードベースに基づく最後のメジャーリリース** であり、Go 言語で書き直される TypeScript 7.0 への移行を円滑にするための橋渡しリリースとして位置づけられている。GA は 3月17日を予定。

多数のデフォルト値変更と非推奨機能の削除を含み、モダンな設定への移行を促すことで、TypeScript 7.0 でのネイティブコンパイラへの切り替えに備える。

## 主な変更点

### 新機能

- **コンテキスト感度の低減**: メソッド構文の関数で `this` が未使用の場合、パラメータ型推論がより効果的に機能
- **`#/` から始まるサブパスインポート**: Node.js の `"#": "./dist/index.js"` のようなシンプルなマッピングをサポート
- **ES2025 API 対応**:
  - `RegExp.escape()`
  - `Promise.try()`
  - Temporal API
  - Map/WeakMap の `getOrInsert`、`getOrInsertComputed`
- **DOM 型の統合**: `dom.iterable` と `dom.asynciterable` が `dom` ライブラリに統合（個別指定が不要に）
- **`--stableTypeOrdering` フラグ**: TypeScript 6.0 と 7.0 間の出力差異を診断するためのフラグ（パフォーマンスに影響あり）

### デフォルト値の変更

| オプション | 旧デフォルト | 新デフォルト |
|-----------|-------------|-------------|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | `es3` | `es2025` |
| `types` | （自動検出） | `[]`（空配列） |
| `rootDir` | （推論） | `.`（固定） |

### 廃止・削除された機能

- `target: es5` — ES5 出力のサポート終了
- `--moduleResolution node`（`node10`） — 旧 Node.js 解決アルゴリズム
- `--moduleResolution classic` — クラシック解決アルゴリズム
- `--baseUrl` — `paths` 内に統合
- AMD / UMD / SystemJS モジュール出力
- `--outFile` — バンドル出力
- `--downlevelIteration` — イテレータのダウンレベル変換
- `esModuleInterop: false` / `allowSyntheticDefaultImports: false` — 常に有効に

## 破壊的変更・移行ガイド

### 1. `types` フィールドの明示指定

デフォルトが `[]` に変更されたため、`@types/*` パッケージを使用している場合は `tsconfig.json` で明示的に指定する必要がある。

```json
{
  "compilerOptions": {
    "types": ["node", "jest"]
  }
}
```

### 2. `rootDir` の設定

ソースファイルが `tsconfig.json` より深い階層にある場合、明示的に `rootDir` を設定する。

```json
{
  "compilerOptions": {
    "rootDir": "./src"
  }
}
```

### 3. import assertions → import attributes

```typescript
// Before
import data from "./data.json" assert { type: "json" };

// After
import data from "./data.json" with { type: "json" };
```

### 4. `baseUrl` から `paths` への移行

```json
// Before
{
  "compilerOptions": {
    "baseUrl": "./src",
    "paths": { "@/*": ["./*"] }
  }
}

// After
{
  "compilerOptions": {
    "paths": { "@/*": ["./src/*"] }
  }
}
```

### 5. モジュール出力の移行

AMD / UMD / SystemJS を使用している場合は ESM に移行し、バンドラー（Vite, esbuild, webpack 等）でのバンドルに切り替える。

## 今後の注目点

- **TypeScript 6.0 GA**: 2026年3月17日に正式リリース予定
- **TypeScript 7.0**: Go で書かれたネイティブコンパイラ。ビルド速度が最大10倍改善される見込み。エディタの言語サービスも Go ベースに移行予定
- **移行戦略**: TypeScript 6.0 で非推奨警告に対処しておくことで、7.0 への移行がスムーズになる。`--stableTypeOrdering` フラグで出力差異を事前に検証可能
- **エコシステムへの影響**: `target: es5` や AMD/UMD 出力の廃止により、レガシーブラウザサポートやレガシーモジュールシステムからの完全な脱却が求められる
