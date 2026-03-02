# TypeScript 6.0 Beta — Go リライトへの移行準備

- **日付**: 2026-02-11
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/), [InfoQ](https://www.infoq.com/news/2026/02/typescript-6-released-beta/), [移行ガイド (GitHub Gist)](https://gist.github.com/privatenumber/3d2e80da28f84ee30b77d53e1693378f)

## 概要

TypeScript 6.0 Beta は 2026-02-11 にリリースされた。**JavaScript ベースのコンパイラとしては最後のリリース**であり、TypeScript 7.0（Go によるフルリライト、プロジェクト名「Corsa」）への移行を準備する位置づけ。新機能の追加よりも、技術的負債の解消・非推奨化・デフォルト値の標準化に重点を置いた「移行リリース」としての性格が強い。

## 主な変更点

### 新機能

- **型推論の改善**: メソッドの型推論が強化
- **Subpath imports (`#/`)**: Node.js のモジュール仕様に準拠した `package.json` の `imports` フィールドをサポート
- **ES2025 ターゲット/ライブラリ**: `es2025` が新しいデフォルトターゲット
- **Temporal API 型**: ECMAScript Temporal API の型定義を組み込み
- **RegExp.escape**: ECMAScript Stage 4 の RegExp Escaping プロポーザルをサポート
- **Map upsert メソッド**: `getOrInsert` / `getOrInsertComputed` の型定義追加
- **DOM Iterable 改善**: DOM 型定義の適切な Iterable サポート

### デフォルト値の変更

| 設定 | 旧デフォルト | 新デフォルト |
|------|-------------|-------------|
| `strict` | `false` | **`true`** |
| `module` | (プロジェクト依存) | **`esnext`** |
| `target` | (プロジェクト依存) | **`es2025`** |
| モジュール解決 | (プロジェクト依存) | **ES Modules** |

## 破壊的変更・移行ガイド

### 非推奨化された機能

以下の機能は TypeScript 6.0 で非推奨（deprecation warning）となり、**TypeScript 7.0 で完全に削除**される予定：

| 非推奨項目 | 対応方法 |
|-----------|---------|
| ES5 ターゲット | `es2015` 以上に変更 |
| AMD / UMD モジュール | ESM または CommonJS に移行 |
| `baseUrl` | `paths` + `rootDirs` で代替 |
| `outFile` バンドリング | 外部バンドラー（Vite, esbuild 等）を使用 |
| `--downlevelIteration` | ターゲットを es2015+ に引き上げ |
| `--moduleResolution node` | `node16` または `bundler` に変更 |
| `--moduleResolution classic` | `node16` または `bundler` に変更 |
| `--esModuleInterop false` | `true` に変更（デフォルト） |
| `--alwaysStrict false` | `strict: true` で包含 |
| レガシー名前空間構文 | ES モジュール構文に移行 |

### 移行戦略

1. **即座の対応は不要**: `"ignoreDeprecations": "6.0"` を `tsconfig.json` に追加することで、非推奨の機能を引き続きエラーなしで使用可能
2. **段階的な移行を推奨**: TypeScript 7.0 では非推奨機能が完全削除されるため、6.0 の期間中に移行作業を進めることが強く推奨される
3. **feature stable**: 6.0 Beta の時点で機能は確定しており、新機能や追加の破壊的変更は計画されていない

```jsonc
// tsconfig.json — 一時的な非推奨抑制
{
  "compilerOptions": {
    "ignoreDeprecations": "6.0",
    // 既存の設定をそのまま維持
  }
}
```

## 今後の注目点

- **TypeScript 6.0 正式リリース**: Beta の時点で feature complete。数週間以内にプロダクションリリース予定
- **TypeScript 7.0（Project Corsa）**: Go によるフルリライト。ビルド時間 5〜10 倍高速化、メモリ使用量約 50% 削減を目標。2026 年中旬〜後半（夏頃）にリリース予定
- **エコシステムへの影響**: strict デフォルト化により、新規プロジェクトのコード品質がベースラインで向上。ES5 ターゲット廃止は IE サポートの正式な終焉を意味する
