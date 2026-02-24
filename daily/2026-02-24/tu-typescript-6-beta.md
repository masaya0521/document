# TypeScript 6.0 Beta — JavaScript ベース最後のリリース

- **日付**: 2026-02-11
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/), [InfoQ](https://www.infoq.com/news/2026/02/typescript-6-released-beta/), [GitHub Releases](https://github.com/microsoft/typescript/releases)

## 概要

TypeScript 6.0 Beta は、現在の JavaScript コードベースに基づく**最後のメジャーリリース**である。Go 言語で書き直された TypeScript 7.0 への橋渡しとして位置づけられており、多数のデフォルト値変更と非推奨化が含まれる。strict モードがデフォルトで有効化され、ES5 ターゲットや AMD/UMD モジュールなどレガシーオプションが非推奨となった。安定版は 2026年3月17日にリリース予定。

## 主な変更点

### 新機能

- **`this` なし関数の文脈感受性の低減**: メソッド構文の関数でも `this` が使用されていなければ型推論が改善
- **サブパスインポート `#/` 対応**: Node.js の `"imports"` フィールドで `"#/"` プレフィックスをサポート
- **`--moduleResolution bundler` + `--module commonjs` の組み合わせ対応**: 従来の制限が解除
- **新しい API 型定義**: Temporal API、Map/WeakMap の `getOrInsert`/`getOrInsertComputed`、`RegExp.escape`、ES2025 サポート
- **DOM lib の統合**: `lib.dom` に `dom.iterable` と `dom.asynciterable` を統合

### デフォルト値の変更

| オプション | 旧デフォルト | 新デフォルト | 影響 |
|-----------|------------|------------|------|
| `strict` | `false` | `true` | より厳密な型チェックがデフォルトに |
| `module` | `commonjs` | `esnext` | ESM がデフォルトに |
| `target` | `es2020` | `es2025` | 最新仕様対応 |
| `types` | 全 `@types` | `[]` | 必要な型のみ明示的に指定が必要 |
| `rootDir` | 推論 | `.`（設定ファイル所在地） | 明示的指定が必要に |

## 破壊的変更・移行ガイド

### 非推奨化されたオプション

以下のオプションは非推奨となり、使用すると警告が表示される。`"ignoreDeprecations": "6.0"` で一時的に抑制可能。

1. **`--target es5`** → ES2015 以上が必須。下位互換が必要な場合は外部コンパイラ（Babel 等）を使用
2. **`--downlevelIteration`** → ES5 廃止に伴い不要に
3. **`--moduleResolution node`（node10）** → `nodenext` または `bundler` に移行
4. **`--module amd/umd/systemjs`** → ESM 採用が必須
5. **`--baseUrl`** → `paths` に統合。パスを相対パスで明示的に指定
6. **`--moduleResolution classic`** → 削除
7. **`--outFile`** → 外部バンドラー利用が必須
8. **`esModuleInterop: false` / `allowSyntheticDefaultImports: false`** → 常に有効化

### コード構文の非推奨化

```typescript
// ❌ 非推奨: module 構文
module Foo {
    export const bar = 10;
}

// ✅ 推奨: namespace
namespace Foo {
    export const bar = 10;
}

// ❌ 非推奨: asserts キーワード
import blob from "./file.json" asserts { type: "json" }

// ✅ 推奨: with キーワード
import blob from "./file.json" with { type: "json" }
```

### 移行手順

**1. `tsconfig.json` のデフォルト値変更に対応**

```json
{
  "compilerOptions": {
    "types": ["node", "jest"],
    "rootDir": "./src"
  }
}
```

**2. `baseUrl` 削除時のパス修正**

```json
// Before
{
  "baseUrl": "./src",
  "paths": {
    "@app/*": ["app/*"],
    "@lib/*": ["lib/*"]
  }
}

// After
{
  "paths": {
    "@app/*": ["./src/app/*"],
    "@lib/*": ["./src/lib/*"]
  }
}
```

**3. 段階的対応**

- まず `"ignoreDeprecations": "6.0"` で警告を抑制し、既存プロジェクトを 6.0 で動作させる
- 非推奨オプションを順次削除していく
- TypeScript 7.0 リリース前に対応を完了する

### `--stableTypeOrdering` フラグ

6.0 から 7.0 への移行時に型の順序が不安定になる可能性があるため、6.0 で 7.0 と同じ動作に統一するフラグが用意された。ただしビルド時間が最大 25% 増加する可能性があり、長期使用は非推奨。

## 今後の注目点

- **TypeScript 7.0**: Go 言語による新実装。6.0 直後にリリース予定。5-10x のコンパイル高速化、約 8x のエディタ起動改善、約 50% のメモリ削減が期待される
- **6.0 安定版**: 2026年3月17日リリース予定
- **移行期間**: 6.0 は「feature stable」であり、新機能や追加の破壊的変更は計画されていない。7.0 への移行に集中できる
