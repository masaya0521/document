# TypeScript 6.0 Beta — JS ベース最終リリースと TS 7.0 への移行準備

- **日付**: 2026-02-11
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/), [InfoWorld](https://www.infoworld.com/article/4131798/last-javascript-based-typescript-arrives-in-beta.html)

## 概要

TypeScript 6.0 Beta は2026年2月11日に発表された、JavaScript ベースのコンパイラとしては**最後のリリース**となる歴史的なバージョン。TypeScript 7.0 は Go で書き直されたコンパイラ（Project Corsa）に移行し、ネイティブコードと共有メモリマルチスレッドにより大幅なパフォーマンス向上が見込まれる。6.0 は ES2025 サポート、Temporal API 型、多数のデフォルト設定の見直しを含み、7.0 への移行を円滑にするための `--stableTypeOrdering` フラグが導入されている。正式リリースは2026年3月17日予定。

## 主な変更点

### 新機能

#### ES2025 ターゲットとライブラリ

`target` と `lib` に `es2025` を指定可能に。以下の新しいビルトイン API が含まれる：

- `RegExp.escape`
- ECMAScript **Temporal API** の完全な型定義
- Map の `getOrInsert`, `getOrInsertComputed` メソッド

#### `--stableTypeOrdering` フラグ

TypeScript 7.0（Go ベース）では並列処理により型の出力順序が非決定的になる可能性がある。このフラグを有効にすると 6.0 の段階で 7.0 の決定的な型順序に合わせることができ、移行前の差分検証に役立つ。

```json
{
  "compilerOptions": {
    "stableTypeOrdering": true
  }
}
```

#### `this` を使わない関数のコンテキスト感度改善

関数内で `this` を使用していない場合、コンテキスト敏感として扱われなくなった。オブジェクトリテラル内のプロパティ順序に依存しない、より良い型推論が可能に。

#### サブパスインポート `#/` サポート

Node.js のサブパスインポート（`#/` で始まるもの）をサポート。パスマッピングがシンプルに。

```json
{
  "imports": {
    "#": "./dist/index.js",
    "#/*": "./dist/*"
  }
}
```

#### `--moduleResolution bundler` と CommonJS の組み合わせ

以前は ESM に限定されていた `--moduleResolution bundler` が `--module commonjs` との組み合わせでも利用可能に。

#### DOM ライブラリの統合

`dom` lib に `dom.iterable` と `dom.asynciterable` が自動で含まれるようになった。

## 破壊的変更・移行ガイド

### デフォルト設定の大幅変更

TypeScript 6.0 では多くのデフォルト値が変更された。既存プロジェクトへの影響が大きいため注意が必要。

| 設定 | 旧デフォルト | 新デフォルト |
|------|------------|------------|
| `strict` | `false` | **`true`** |
| `module` | 状況依存 | **`esnext`** |
| `target` | `es5` | **`es2025`** |
| `rootDir` | 推論 | **`tsconfig.json` のディレクトリ** |
| `types` | 全 `@types` 含む | **`[]`（空配列）** |

### 非推奨化・削除されたオプション

**非推奨化：**
- `target: es5` — ES5 ターゲットは非推奨
- `--moduleResolution node` (`node10`) — 非推奨
- `--baseUrl` — 非推奨
- `--downlevelIteration` — 非推奨
- `--alwaysStrict false` — 非推奨

**削除：**
- `--outFile` — 完全削除
- AMD, UMD, SystemJS の `module` 値 — 削除
- `--moduleResolution classic` — 削除
- レガシー `module` 名前空間構文 → `namespace` キーワードに統一

**動作変更：**
- `esModuleInterop: false` と `allowSyntheticDefaultImports: false` の指定が不可に
- Import `asserts` 構文 → `with` 構文に置き換え

### 一時的な非推奨警告の抑制

`tsconfig.json` に以下を追加することで、非推奨警告を一時的に抑制できる：

```json
{
  "compilerOptions": {
    "ignoreDeprecations": "6.0"
  }
}
```

### 移行手順

1. **`--stableTypeOrdering` を有効化**して、TS 7.0 への移行に備える
2. 非推奨オプション（`target: es5`, `--baseUrl`, `--moduleResolution node`）の使用を見直す
3. AMD/UMD/SystemJS モジュール形式を使用している場合は ESM への移行を検討
4. `strict: true` がデフォルトになるため、既存プロジェクトでは明示的に `strict: false` を指定するか、strict モードに対応する
5. `types` が空配列になるため、必要な `@types` パッケージを明示的に列挙する

## 今後の注目点

- **TypeScript 6.0 正式リリース**: 2026年3月17日予定
- **TypeScript 7.0**（Go ベースコンパイラ）: 2026年中旬リリース目標
  - ビルド速度が最大10倍に改善される見込み
  - 共有メモリマルチスレッドによる並列型チェック
- TS 7.0 のブレイキングチェンジに関する追加情報
- エコシステム（ESLint, Prettier 等）の対応状況
