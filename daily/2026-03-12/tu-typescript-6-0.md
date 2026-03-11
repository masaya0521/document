# TypeScript 6.0 RC — JS ベース最後のリリースと Go ベース TS 7.0 への道筋

- **日付**: 2026-03-06 (RC)、2026-03-17 (GA 予定)
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/)、[InfoWorld](https://www.infoworld.com/article/4143186/typescript-6-0-reaches-release-candidate-stage.html)

## 概要

TypeScript 6.0 は、現行の JavaScript ベースのコンパイラとしては最後のメジャーリリースとなる。次期 TypeScript 7.0 は Go で書き直された新コンパイラ「Corsa」がベースとなり、5-10 倍の高速コンパイル、約 8 倍のエディタ起動速度改善、約 50% のメモリ削減が見込まれている。TypeScript 6.0 はその橋渡しとして、デフォルト設定の近代化とレガシー機能の削除を大胆に進めた。

## 主な変更点

### 新機能

#### Thisless Functions のコンテキスト推論改善
メソッド構文で記述された関数で `this` を使用していない場合、より高い優先度で型推論が行われるようになった。

```typescript
declare function callIt<T>(obj: {
    produce: (x: number) => T,
    consume: (y: T) => void,
}): void;

// メソッド構文でも正しく推論される
callIt({
    consume(y) { return y.toFixed(); },
    produce(x: number) { return x * 2; },
});
```

#### `#/` プレフィックスによるサブパスインポート
Node.js の subpath imports に対応し、`#/` プレフィックスでの簡潔なインポートが可能に。バンドラーでよく使われる `@/` パターンと同様の記法。

```json
{
    "imports": {
        "#": "./dist/index.js",
        "#/*": "./dist/*"
    }
}
```

#### 新しい組み込み型のサポート
- **Temporal API**: Stage 3 に達した日時処理 API の型定義
- **Map.getOrInsert() / Map.getOrInsertComputed()**: upsert メソッド
- **RegExp.escape**: 正規表現の特殊文字を自動エスケープ

```typescript
const value = compilerOptions.getOrInsert("strict", true);
const escapedWord = RegExp.escape(word);
```

#### `--stableTypeOrdering` フラグ
TypeScript 7.0 (Go ベース) では並列処理により型 ID の順序が非決定的になる可能性がある。このフラグで出力を安定化し、移行を容易にする。

#### `es2025` ターゲット対応
新しい ES2025 の組み込み API 型宣言が利用可能に。

### その他の改善
- DOM 型に `dom.iterable` と `dom.asynciterable` を統合
- `--moduleResolution bundler` で `--module commonjs` の併用が可能に
- `import assert` 構文を `import with` 属性に統一

## 破壊的変更・移行ガイド

TypeScript 6.0 ではデフォルト設定が大幅に変更され、レガシー機能が削除された。多くのプロジェクトで `tsconfig.json` の更新が必要。

### デフォルト値の変更
| 設定 | 旧デフォルト | 新デフォルト |
|------|------------|------------|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | `es3` | `es2025` |
| `types` | 自動検出 | `[]`（明示指定が必要） |

### 削除された機能
- `--module amd|umd|systemjs` — 完全削除
- `--moduleResolution classic` — 完全削除
- `--outFile` — 完全削除
- `esModuleInterop: false` / `allowSyntheticDefaultImports: false` — 廃止

### 非推奨化
- `target: es5`
- `--downlevelIteration`
- `--moduleResolution node10`
- `--baseUrl`
- レガシー `module` キーワード（名前空間用）

### 移行時の典型的な対応

```json
{
    "compilerOptions": {
        "types": ["node"],
        "rootDir": "./src"
    }
}
```

`@types` パッケージを使用しているプロジェクトは `types` フィールドの明示指定が必須になった。

## 今後の注目点

- **TypeScript 7.0 (Corsa)**: 2026 年夏に予定。Go で書き直されたコンパイラにより劇的なパフォーマンス向上
- **`--stableTypeOrdering`** を有効にして TS 7.0 移行の事前検証を行うことが推奨
- TS 6.0 の破壊的変更を早期に適用し、TS 7.0 移行時の差分を最小化するのが賢明
