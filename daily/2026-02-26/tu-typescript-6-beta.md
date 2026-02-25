# TypeScript 6.0 Beta — JS ベースコンパイラの最終メジャーリリース

- **日付**: 2026-02-11
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/), [InfoQ](https://www.infoq.com/news/2026/02/typescript-6-released-beta/)

## 概要

TypeScript 6.0 Beta は、現在の JavaScript ベースコンパイラでの最後のメジャーリリースとなる。TypeScript 7.0 では Go 言語で書き直されたコンパイラが採用され、5〜10 倍のビルド速度、約 8 倍のエディタ起動時間短縮、約 50% のメモリ削減が見込まれている。

TS 6.0 はその「橋渡し」として機能し、デフォルト設定の近代化と非推奨機能の整理に焦点を当てている。`npm install -D typescript@beta` でインストール可能。

## 主な変更点

### デフォルト設定の変更

| 設定項目 | 旧デフォルト | 新デフォルト |
|---------|------------|------------|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | `es3` | `es2025` |
| `types` | (全自動取得) | `[]`（空配列） |
| `rootDir` | 推論 | `tsconfig.json` の親ディレクトリ |

これにより、新しいプロジェクトはデフォルトでモダンな設定になるが、既存プロジェクトでは `tsconfig.json` の明示的な設定が必要になる場合がある。

### 新機能

#### サブパスインポート (`#/` プレフィックス)

Node.js のモジュール仕様に対応し、`package.json` の `imports` フィールドをサポート:

```json
{
  "imports": {
    "#": "./dist/index.js",
    "#/*": "./dist/*"
  }
}
```

これにより、`baseUrl` やカスタムパスマッピングへの依存が減る。

#### ES2025 サポート

- `RegExp.escape()` (Stage 4 ECMAScript proposal)
- Temporal API の型定義
- DOM 型定義での Iterable サポート改善

#### Map/WeakMap の `upsert` メソッド

```typescript
// 従来: has → get/set の2段階
if (!map.has("strict")) {
  map.set("strict", true);
}
const value = map.get("strict");

// TS 6.0: getOrInsert で1行
const value = compilerOptions.getOrInsert("strict", true);
```

#### 文脈感度の改善

`this` を使用しない関数が文脈的に敏感でなくなり、メソッド構文とアロー関数の型推論が統一された:

```typescript
callIt({
  // メソッド構文でも正しく型推論される
  consume(y) { return y.toFixed(); },
  produce(x: number) { return x * 2; },
});
```

## 破壊的変更・移行ガイド

### 非推奨化された機能

以下の機能は TS 6.0 で非推奨となり、TS 7.0 で完全に削除される予定:

- `target: "es5"` — モダンブラウザ前提のプロジェクトでは不要
- `--downlevelIteration` — ES5 ターゲット廃止に伴い不要
- `--moduleResolution: "node"` — `"node16"` または `"bundler"` への移行を推奨
- `--baseUrl` — サブパスインポートで代替可能
- `--outFile` — バンドラーの使用を推奨
- AMD / UMD / SystemJS モジュール形式
- `module` キーワード — `namespace` への移行を推奨

### 一時的な抑制

非推奨警告は `"ignoreDeprecations": "6.0"` で一時的に抑制可能:

```json
{
  "compilerOptions": {
    "ignoreDeprecations": "6.0",
    "target": "es5"
  }
}
```

ただし、この設定は TS 7.0 では使用できなくなるため、早期の移行が推奨される。

### 移行チェックリスト

1. `tsconfig.json` で `types` を明示的に設定する（例: `["node", "jest"]`）
2. `rootDir` を明示的に設定する（例: `"./src"`）
3. `moduleResolution` を `"node16"` または `"bundler"` に変更する
4. `baseUrl` を使用している場合、サブパスインポートへの移行を検討する
5. `target: "es5"` を使用している場合、`"es2020"` 以上への変更を検討する

## 今後の注目点

- **TypeScript 7.0**: Go ベースコンパイラのリリースは 2026 年中盤〜後半を予定。エディタサポート（Language Service）も Go に移行予定
- **エコシステムへの影響**: `tsc` の API を直接使用しているツール（`ts-morph` 等）は TS 7.0 で大幅な対応が必要になる可能性
- **段階的移行**: TS 6.0 の非推奨警告に対応することで、TS 7.0 への移行がスムーズになる設計
