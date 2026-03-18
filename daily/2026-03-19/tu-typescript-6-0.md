# TypeScript 6.0 — JS ベース最後のメジャーリリース

- **日付**: 2026-03-17（GA）
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [InfoWorld](https://www.infoworld.com/article/4143186/typescript-6-0-reaches-release-candidate-stage.html)

## 概要

TypeScript 6.0 は、現行の JavaScript ベースコンパイラにおける最後のメジャーリリースである。次期 TypeScript 7.0 では Go 言語で書き直されたコンパイラ・言語サービスが基盤となり、共有メモリによるマルチスレッド型チェックで大幅な高速化が見込まれている。TypeScript 6.0 はその 5.x 系と 7.0 の間の「橋渡し」として位置付けられ、多数のデフォルト変更と非推奨化により、エコシステム全体の 7.0 移行を準備する。

## 主な変更点

### 新しいデフォルト設定

TypeScript 6.0 では複数のコンパイラオプションのデフォルトが変更された。

- **`strict: true`**（旧: `false`） — strict モードがデフォルトに
- **`module: esnext`**（旧: `commonjs`） — ESM がデフォルトモジュール
- **`target: es2025`**（旧: 固定値） — 毎年のリリースに合わせて浮動する方式に
- **`types: []`**（旧: `@types` 全列挙） — 明示的な指定が必要に
- **`rootDir: .`**（旧: 推論） — 明示的にカレントディレクトリ

### 新機能

- **Temporal API 型サポート**: Stage-3 の Temporal プロポーザルに対する完全な型定義を提供
- **es2025 target/lib**: `RegExp.escape()` や Temporal API 等の ES2025 機能をサポート
- **Map/WeakMap upsert メソッド**: Stage-4 の `getOrInsert` / `getOrInsertComputed` に対応
- **DOM ライブラリ統合**: `dom` に `dom.iterable` と `dom.asynciterable` がデフォルトで含まれるように
- **サブパスインポートの `#/` プレフィックス**: Node.js 互換の簡易パス指定
- **this を使わない関数のコンテキスト感度低減**: ジェネリック型推論が柔軟に

### `--stableTypeOrdering` フラグ

TypeScript 7.0（Go ベース）では型の内部順序が決定的アルゴリズムに変更される。このフラグを有効にすると 6.0 の出力を 7.0 と揃えて比較できるが、最大 25% のパフォーマンスオーバーヘッドがあるため、移行検証時のみの使用が推奨される。

## 破壊的変更・移行ガイド

### 非推奨化（7.0 で完全削除予定）

以下のオプションは `ignoreDeprecations: '6.0'` で一時的に抑制可能だが、7.0 では完全に削除される。

| 非推奨オプション | 移行先 |
|---|---|
| `target: es5` / `--downlevelIteration` | `es2020` 以上に引き上げ |
| `--moduleResolution node` | `nodenext` または `bundler` |
| `--baseUrl` | `paths` のルート相対パスに変更 |
| `amd` / `umd` / `systemjs` module | `esnext` + 外部バンドラー |
| `--outFile` | 外部バンドラーを使用 |
| `module` 名前空間構文 | `namespace` キーワードに統一 |
| `esModuleInterop: false` | `true` に変更 |
| `allowSyntheticDefaultImports: false` | `true` に変更 |

### 典型的な移行作業

```jsonc
// tsconfig.json の調整例
{
  "compilerOptions": {
    "types": ["node"],           // 明示的に指定が必要に
    "rootDir": "./src",          // 推論に頼らず明示化
    "moduleResolution": "nodenext" // "node" からの移行
  }
}
```

## 今後の注目点

- **TypeScript 7.0**: Go ベースコンパイラの初リリース。共有メモリマルチスレッドによる並列型チェックで、大規模プロジェクトでの劇的な速度改善が期待される
- **エコシステム対応**: `@types` パッケージや主要フレームワークの 6.0 デフォルト変更への対応状況
- **`ignoreDeprecations` の期限**: 6.0 で非推奨となった機能は 7.0 で完全削除されるため、早期の移行対応が重要
