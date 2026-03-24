# TypeScript 6.0 — JS ベース最終リリースと Go ベース v7.0 への移行準備

- **日付**: 2026-03-23
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [RC 発表](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [GitHub Releases](https://github.com/microsoft/typescript/releases)

## 概要

TypeScript 6.0 は、現行の JavaScript コードベースに基づく最後のメジャーリリースである。次期 TypeScript 7.0 は Go 言語で書き直されたネイティブコンパイラ（コードネーム "Corsa"）を基盤とし、5-10x のコンパイル高速化、8x のエディタ起動改善、約 50% のメモリ削減が見込まれている。

6.0 はその橋渡し的リリースとして位置づけられ、多くのデフォルト値変更と非推奨オプションの整理が行われた。7.0 への移行をスムーズにするため、6.0 で全ての非推奨警告を解消しておくことが推奨される。

## 主な変更点

### 新機能

- **`this` を使用しない関数の推論改善**: メソッド構文で記述されていても `this` を使わない場合、型推論がより適切に処理される。ジェネリック関数呼び出しにおけるプロパティ順序に依存しない推論が実現
- **サブパスインポートで `#/` をサポート**: Node.js の最新仕様に対応し、`package.json` の `imports` フィールドで `#/*` プレフィックスが使用可能に
- **ES2025 ターゲット追加**: `RegExp.escape`、`Promise.try` などの新しい API 型定義をサポート
- **Temporal API の型サポート**: Stage 4 に到達した Temporal 提案の型定義が組み込み
- **Map/WeakMap の upsert メソッド**: `getOrInsert` と `getOrInsertComputed` でキー存在チェックと値設定が簡潔に
- **DOM lib の統合**: `lib.dom` が `dom.iterable` と `dom.asynciterable` を完全に含むようになり、複数の lib 指定が不要に

### デフォルト値の変更

| 設定 | 旧デフォルト | 新デフォルト |
|------|-------------|-------------|
| `strict` | `false` | `true` |
| `module` | - | `esnext` |
| `target` | - | `es2025` |
| `types` | 全 `@types` を列挙 | `[]`（空配列） |

## 破壊的変更・移行ガイド

### 非推奨化されたオプション

| オプション | 理由 |
|-----------|------|
| `target: es5` | ES5 向けのダウンレベルは不要に |
| `--downlevelIteration` | ES5 に依存 |
| `--moduleResolution node` | Node.js 10 仕様は古い |
| `--module amd/umd/systemjs` | ESM が標準化 |
| `--baseUrl` | `paths` で直接指定可能 |
| `esModuleInterop: false` | 相互運用性の問題 |
| `--outFile` | バンドラーの方が優れている |

### 移行時の重要な調整

**1. `types` フィールドの明示的指定**

デフォルトが空配列になったため、Node.js や Jest 等の型を使用する場合は明示的に指定が必要:

```json
{
  "compilerOptions": {
    "types": ["node", "jest"]
  }
}
```

**2. `rootDir` の明示的指定**

デフォルトが `tsconfig.json` のディレクトリに統一された。ソースファイルが `src/` にある場合:

```json
{
  "compilerOptions": {
    "rootDir": "./src"
  }
}
```

**3. `--stableTypeOrdering` フラグ**

6.0 → 7.0 移行時に型の順序が変わる可能性がある。このフラグで 7.0 の動作に合わせられるが、型チェックが最大 25% 遅くなる可能性あり。

## 今後の注目点

- **TypeScript 7.0**: Go ベースのネイティブコンパイラ。2026 年夏頃リリース見込み。`@typescript/native-preview` パッケージで先行体験可能
- **パフォーマンス**: 5-10x のコンパイル高速化、ほぼ即時のインクリメンタルビルド、8x のエディタ起動改善
- **メモリ**: 約 50% のメモリ使用量削減
- **互換性**: 6.0 で非推奨警告を全て解消しておくことで、7.0 へのスムーズな移行が可能
