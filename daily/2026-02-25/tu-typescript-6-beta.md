# TypeScript 6.0 Beta — JavaScript ベース最後のリリースと Go 移行への道

- **日付**: 2026-02-11
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/), [InfoQ](https://www.infoq.com/news/2026/02/typescript-6-released-beta/)

## 概要

TypeScript 6.0 Beta は、現在の JavaScript コードベースに基づく **最後のメジャーリリース** となる。次期 TypeScript 7.0 は Go で書き直されたネイティブコンパイラとなり、最大 10 倍のビルド高速化が見込まれる。TypeScript 6.0 はその移行を円滑にするためのブリッジリリースであり、多数のデフォルト値変更・非推奨化を含む。

インストール: `npm install -D typescript@beta`

## 主な変更点

### デフォルト値の大幅変更

| オプション | 旧デフォルト | 新デフォルト |
|---------|---------|---------|
| `strict` | `false` | **`true`** |
| `module` | `commonjs` | **`esnext`** |
| `target` | `es5` | **`es2025`** |
| `types` | すべてを列挙 | **`[]`（空配列）** |
| `rootDir` | 推論 | **`tsconfig.json` のディレクトリ** |
| `noUncheckedSideEffectImports` | `false` | **`true`** |

特に `types` フィールドの変更により、20〜50% のパフォーマンス改善が期待できる。必要な型定義のみを明示的に指定する形式になった。

```json
{
  "compilerOptions": {
    "types": ["node", "jest"]
  }
}
```

### 新しい言語機能サポート

**ES2025 対応:**
- `RegExp.escape()` — 正規表現文字のエスケープ
- `Temporal API` — 日付・時刻の新しい標準 API
- `Map/WeakMap upsert メソッド` — `getOrInsert()`, `getOrInsertComputed()`

```typescript
// RegExp.escape
const escapedWord = RegExp.escape(word);
const regex = new RegExp(`\\b${escapedWord}\\b`, "g");

// Temporal API
let tomorrow = Temporal.Now.instant().add({ hours: 24 });

// Map upsert
let value = compilerOptions.getOrInsert("strict", true);
someMap.getOrInsertComputed(key, () => computeExpensiveValue());
```

**DOM ライブラリの統合:**

`dom.iterable` と `dom.asynciterable` が `dom` に統合。別途指定が不要になった。

### その他の改善

- **`this` なし関数の文脈感度改善** — メソッド構文でのジェネリック型推論が改善
- **サブパスインポートで `#/` をサポート** — Node.js 最新仕様に対応
- **`--moduleResolution bundler` と `--module commonjs` の組み合わせ** が許可
- **`--stableTypeOrdering` フラグ** — TypeScript 7.0 への移行支援用（型の順序を決定的に）

## 破壊的変更・移行ガイド

### 非推奨化された機能一覧

以下の機能が非推奨となり、**TypeScript 7.0 で完全に削除** される予定:

| 機能 | 理由 |
|-----|------|
| `target: es5` | レガシー IE の廃止、evergreen ブラウザが標準 |
| `--downlevelIteration` | ES5 削除に伴い不要 |
| `--moduleResolution node`（node10） | Node.js 10 の古いアルゴリズム |
| `--module amd/umd/systemjs` | ESM が普遍化 |
| `--baseUrl` | パス設定では不要 |
| `--moduleResolution classic` | 歴史的経緯のみ |
| `--outFile` | 外部バンドラーで実施 |
| `import asserts` | `with` 構文に統一 |

### CLI 動作の変更

`tsconfig.json` が存在する場合、ファイルを直接指定するとエラーになる:

```bash
# 従来は成功 → TypeScript 6.0 ではエラー
tsc foo.ts

# 新しい方法
tsc --ignoreConfig foo.ts
```

### 移行時の一時的回避策

TypeScript 5.9 からの移行時に、`tsconfig.json` に以下を追加することで非推奨警告を抑制可能:

```json
{
  "ignoreDeprecations": "6.0"
}
```

ただし TypeScript 7.0 では非推奨機能が完全削除されるため、早期の対応が推奨される。

### 推奨される移行手順

1. `npm install -D typescript@beta` でインストール
2. `tsc --noEmit` でエラーと非推奨警告を確認
3. 自動化ツール（`ts5to6` 等）で `baseUrl` と `rootDir` を自動調整
4. 非推奨オプションを段階的に置き換え
5. `"ignoreDeprecations": "6.0"` は一時的にのみ使用し、本対応を進める

## 今後の注目点

- **TypeScript 7.0**（2026 年中盤予定）: Go ベースのネイティブコンパイラ。最大 10 倍のビルド高速化
- **`--stableTypeOrdering`** を有効にして TypeScript 7.0 との型出力の互換性を事前検証可能
- TypeScript 7.0 では `strict` がデフォルト有効、ES5 ターゲット完全削除、AMD/UMD/SystemJS 削除が確定
- エディタ・言語サーバーも Go ベースに移行予定で、IDE 体験の大幅改善が見込まれる
