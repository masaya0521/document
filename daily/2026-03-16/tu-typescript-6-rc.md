# TypeScript 6.0 RC — JS ベース最後のリリースと移行ガイド

- **日付**: 2026-03-06（RC）、2026-03-17（GA 予定）
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [InfoWorld](https://www.infoworld.com/article/4143186/typescript-6-0-reaches-release-candidate-stage.html)

## 概要

TypeScript 6.0 は現行の JavaScript ベースコンパイラによる最後のメジャーリリースとなる。次期 TypeScript 7.0 では Go で書き直されたネイティブコンパイラ「Corsa」が導入され、5〜10 倍のコンパイル速度向上が見込まれている。

6.0 はその橋渡しとして、デフォルト設定のモダン化と古い出力形式の廃止を行い、7.0 との動作差異を最小化する重要なリリースである。

## 主な変更点

### 新 API 対応
- **Temporal API**: Stage 3 の日時処理 API に対する組み込み型定義を追加。イミュータブルな日時操作、タイムゾーン対応、ナノ秒精度をサポート
- **Map.getOrInsert**: Map に対するキー存在確認と挿入を一括で行うメソッド
- **RegExp.escape**: 正規表現の特殊文字をエスケープする関数（ES2025 Stage 4）

### 型推論の改善
- メソッド構文での型推論が強化
- `this` が未使用の関数は文脈感応的ではなくなり、プロパティの順序に依存しない推論が可能に
- ジェネリック JSX 式における関数式の型チェック調整（7.0 の動作に合わせる）

### モジュール関連
- `#/` で始まるサブパスインポートが Node.js 20 以降で対応
- `--moduleResolution bundler` と `--module commonjs` の組み合わせが新たに許可

## 破壊的変更・移行ガイド

### デフォルト値の変更（最大の影響）

| オプション | 旧デフォルト | 新デフォルト |
|-----------|-------------|-------------|
| `strict` | `false` | **`true`** |
| `module` | `commonjs` | **`esnext`** |
| `target` | `es3` | **`es2025`** |
| `types` | （全 @types 自動読込） | **`[]`（空配列）** |

**`types: []` の影響が特に大きい。** 未指定の場合 `@types` パッケージが自動読み込みされなくなるため、多くのプロジェクトで `"types": ["node"]` 等の明示的な設定が必要になる。

### 削除される機能
- `target: es5`（ES2015 が最低要件に）
- AMD、UMD、SystemJS 出力
- `--outFile` オプション
- `--baseUrl`（パスマッピングは `paths` で対応）

### 移行手順

1. **`types` フィールドを明示的に設定**: `"types": ["node", "jest"]` 等
2. **`rootDir` を明示化**: 未指定時は `tsconfig.json` のあるディレクトリがデフォルトに
3. **`strict` モード対応**: 既存コードで型エラーが増加する可能性あり
4. **段階的移行**: 廃止予定オプションは `"ignoreDeprecations": "6.0"` で一時的に無効化可能

```jsonc
// tsconfig.json の移行例
{
  "compilerOptions": {
    "types": ["node"],        // 明示的に指定
    "rootDir": "./src",       // 明示化推奨
    "ignoreDeprecations": "6.0"  // 段階的移行用（一時的）
  }
}
```

## 今後の注目点

- **TypeScript 7.0**（2026 年中後半予定）: Go ベースのネイティブコンパイラ「Corsa」導入
  - 5〜10 倍のコンパイル速度向上
  - ほぼ即座のインクリメンタルビルド
  - メモリ使用量 50% 削減
- 6.0 GA は 2026-03-17 にリリース予定
- エコシステム（ESLint, Prettier, IDE プラグイン等）の 6.0 対応状況に注目
