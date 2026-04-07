# TypeScript 6.0 — JS ベース最終リリースと Go 書き換えへの移行

- **日付**: 2026-03-23
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [GitHub Releases](https://github.com/microsoft/typescript/releases)

## 概要

TypeScript 6.0 は、現行の JavaScript ベースコンパイラとしての最終メジャーリリースである。次期 TypeScript 7.0 は Go で書き直されたネイティブコンパイラとなり、並列型チェックにより大幅なパフォーマンス向上が見込まれる。6.0 はその移行を円滑に進めるための「橋渡し」リリースとして位置づけられており、多数の破壊的変更と非推奨化が含まれる。

TypeScript 7.0 は「完成に極めて近い」状態であり、VS Code 拡張機能や `@typescript/native-preview` npm パッケージで既に試用可能。数ヶ月以内のリリースが予定されている。

## 主な新機能

### Less Context-Sensitive Functions
`this` を実際に使用していない関数は、型推論時にコンテキスト依存関数として扱われなくなった。メソッド構文でもアロー関数と同等の型推論が機能する。

### Subpath Imports (`#/`)
`package.json` の `imports` フィールドで `#/*` パターンが使用可能に。従来の `#root/*` のような追加セグメントが不要になり、`@/` スタイルの簡潔なパス指定が可能。

### `--stableTypeOrdering` フラグ
型の順序付けを決定的アルゴリズムに基づかせるフラグ。6.0 と 7.0 間の宣言ファイル出力の差異を最小化できる（パフォーマンスへの影響あり）。

### ES2025 対応
- `RegExp.escape`
- `Temporal` API
- `Map.getOrInsert` / `Map.getOrInsertComputed`

### DOM ライブラリ統合
`lib.dom.d.ts` に `dom.iterable` と `dom.asynciterable` が統合され、`lib` の設定が簡潔になった。

## 破壊的変更・移行ガイド

### デフォルト値の変更

| オプション | 旧デフォルト | 新デフォルト |
|-----------|------------|------------|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | - | `es2025`（浮動） |
| `noUncheckedSideEffectImports` | `false` | `true` |

### `types` フィールドの挙動変更
デフォルトが空配列になり、`node_modules/@types` の自動列挙が行われなくなった。`"types": ["node"]` 等の明示が必要。

### `rootDir` の挙動変更
`tsconfig.json` のディレクトリがデフォルトになり、ソースファイルから推論されなくなった。出力先が `./dist/src/` のようになる場合は `"rootDir": "./src"` を明示する。

### 非推奨・廃止された機能

| 機能 | 移行先 |
|------|--------|
| `target: es5` | ES2015 以上にアップグレード |
| `--downlevelIteration` | ES5 廃止に伴い廃止 |
| `--moduleResolution node` | `nodenext` または `bundler` |
| `--module amd/umd/systemjs` | ESM ベースのバンドラー |
| `--baseUrl`（パス解決用） | `paths` エントリに接頭辞を追加 |
| `--moduleResolution classic` | `nodenext` または `bundler` |
| `esModuleInterop: false` | 常に有効化 |
| `--outFile` | 外部バンドラー使用 |
| `import ... assert {}` | `import ... with {}` |

### 推奨される移行手順

1. **TypeScript 6.0 を導入**し、非推奨警告にすべて対応する
2. 急ぎ対応できない場合は `"ignoreDeprecations": "6.0"` で一時的に警告を抑制（7.0 では使用不可）
3. `ts5to6` ツールで `baseUrl` や `rootDir` の設定を自動調整
4. `@typescript/native-preview` で 7.0 を試用し、差分を確認
5. 本移行前に [TypeScript Go リポジトリ](https://github.com/nicolo-ribaudo/TypeScript-Go) へフィードバック

### 推奨 tsconfig 構成

**Web アプリ（バンドラー使用）:**
```json
{
  "compilerOptions": {
    "module": "preserve",
    "moduleResolution": "bundler"
  }
}
```

**Node.js 直接実行:**
```json
{
  "compilerOptions": {
    "module": "nodenext",
    "moduleResolution": "nodenext"
  }
}
```

## 今後の注目点

- **TypeScript 7.0 リリース時期**: 数ヶ月以内。Go 書き換えにより 10x のパフォーマンス向上が期待される
- **型順序の正規化**: 7.0 では内容ベースのソートにより、宣言ファイル出力やエラーメッセージが決定的になる
- **エコシステムへの影響**: ES5 ターゲット廃止により、レガシーブラウザサポートは外部トランスパイラ（Babel 等）に委ねられる
- **`--stableTypeOrdering`**: 6.0 → 7.0 の移行期間中に有効化しておくと、出力差異の確認に役立つ
