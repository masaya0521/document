# TypeScript 6.0 RC — JavaScript ベース最後のリリースと Go 移行への道

- **日付**: 2026-03-07
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog (RC)](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [TypeScript Blog (Beta)](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/), [InfoQ](https://www.infoq.com/news/2026/02/typescript-6-released-beta/)

## 概要

TypeScript 6.0 RC が 2026年3月6日にリリースされた。TypeScript 6.0 は現行の JavaScript コードベースに基づく最後のメジャーリリースであり、TypeScript 7.0 からは Go 言語で書き直されたコンパイラ（Project Corsa）に移行する。6.0 は技術的負債の解消と多数のデフォルト値変更に注力し、7.0 への橋渡しとして設計されている。

## 主な新機能

### `this` を使用しない関数の型推論改善

ジェネリック呼び出し内でメソッド構文で書かれた関数でも、`this` を実際に使用していない場合に型推論が機能するようになった。

```typescript
callIt({
    consume(y) { return y.toFixed(); },
    produce(x: number) { return x * 2; },
});
```

### `#/` サブパスインポート対応

Node.js が新たにサポートした `#/` プレフィックスのサブパスインポートに対応。

```json
{
    "imports": {
        "#": "./dist/index.js",
        "#/*": "./dist/*"
    }
}
```

### ES2025 対応

`RegExp.escape` や Temporal API の型サポートが追加された。

```typescript
const escapedWord = RegExp.escape(word);
let yesterday = Temporal.Now.instant().subtract({ hours: 24 });
```

### Map/WeakMap の `getOrInsert` / `getOrInsertComputed`

```typescript
let value = compilerOptions.getOrInsert("strict", true);
```

### DOM 型の統合

`lib.dom.iterable` と `lib.dom.asynciterable` が `lib.dom` に統合され、別途指定が不要になった。

### `--stableTypeOrdering` フラグ

6.0 と 7.0 間での型順序の違いを診断するための新フラグ。長期的な利用は想定されていない。

## 破壊的変更・移行ガイド

TypeScript 6.0 は多数のデフォルト値変更と非推奨化を含む。**7.0 では非推奨機能が完全に削除される**ため、6.0 での早期移行が推奨される。

### デフォルト値の変更

| オプション | 旧デフォルト | 新デフォルト |
|----------|-----------|----------|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | `es2020` | `es2025` |
| `types` | 全 `@types` 列挙 | `[]`（空配列） |
| `rootDir` | 推論 | `tsconfig.json` のあるディレクトリ |

### 主な非推奨化（12項目）

1. **`target: es5`** — ES2015 以上への移行が必須
2. **`--downlevelIteration`** — ES5 廃止に伴い廃止
3. **`--moduleResolution node`（node10）** — `nodenext` または `bundler` へ移行
4. **`amd`, `umd`, `systemjs` モジュール形式** — 廃止
5. **`--baseUrl`** — `paths` の各エントリに直接プレフィックスを付ける形式へ
6. **`--moduleResolution classic`** — 廃止
7. **`esModuleInterop` / `allowSyntheticDefaultImports`** — 常に有効化
8. **`--alwaysStrict false`** — 全コードがストリクトモード前提
9. **`--outFile`** — 外部バンドラー使用を推奨
10. **`module` キーワード（namespace 構文）** — `namespace` に統一
11. **import assertions（`asserts`）** — `with` 構文に移行
12. **`/// <reference no-default-lib="true"/>`** — `--noLib` または `--libReplacement` を使用

### 一時的な互換性維持

非推奨機能を 6.0 で一時的に使用し続けるには：

```json
{
  "compilerOptions": {
    "ignoreDeprecations": "6.0"
  }
}
```

### 移行チェックリスト

1. `types` フィールドを明示的に指定（例: `"types": ["node", "jest"]`）
2. `rootDir` を明示的に指定（例: `"rootDir": "./src"`）
3. `strict: true` がデフォルトになったことを確認（必要なら `strict: false` を明示）
4. `module` / `target` の新デフォルトを確認
5. import assertions を `with` 構文に書き換え
6. `--moduleResolution` を `nodenext` または `bundler` に変更

## 今後の注目点

- TypeScript 7.0 は Go ベースのコンパイラ（Project Corsa）で、フルビルドで約 10 倍の高速化を実現
- 6.0 で非推奨の機能は 7.0 で完全削除予定
- 7.0 は「6.0 からすぐに公開される見込み」とアナウンスされており、2026年中盤のリリースが予想される
- `--stableTypeOrdering` フラグで 6.0 → 7.0 間の互換性を事前検証可能
