# TypeScript 6.0 — JavaScript ベース最終リリースと 7.0 への移行準備

- **日付**: 2026-03-23
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [GitHub Releases](https://github.com/microsoft/typescript/releases)

## 概要

TypeScript 6.0 は、JavaScript で書かれた TypeScript コンパイラの最終リリースである。Go ネイティブで書き直される TypeScript 7.0 への橋渡しとして位置づけられ、大量の非推奨化とデフォルト値の変更が含まれる。6.0 で非推奨となったオプションは 7.0 で完全に削除される予定のため、早期のアップグレードと対応が推奨される。

## 主な変更点

### デフォルト値の変更

| オプション | 旧デフォルト | 新デフォルト |
|-----------|----------|---------|
| `strict` | `false` | **`true`** |
| `module` | `commonjs` | **`esnext`** |
| `target` | `es2020` | **`es2025`** |
| `types` | すべての `@types` | **`[]`（空配列）** |
| `rootDir` | 推論 | **`tsconfig.json` の親ディレクトリ** |

特に `types` のデフォルトが空配列になったことで、ほとんどのプロジェクトで `"types": ["node"]` の明示的な設定が必要になる。

### 新機能

- **ES2025 サポート**: `RegExp.escape` 等の新しい標準 API に対応
- **Temporal API**: 型定義が組み込みに
- **`#/` サブパスインポート**: Node.js の `#/` で始まるサブパスインポートに `nodenext` / `bundler` で対応
- **`--moduleResolution bundler` + `--module commonjs`**: 組み合わせが可能に
- **DOM ライブラリ統合**: `dom.iterable` と `dom.asynciterable` が `lib.dom.d.ts` に統合

### 型推論の改善

- `this` を使用しない関数がコンテキスト依存と見なされなくなり、メソッド構文とアロー関数の型推論が統一

## 破壊的変更・移行ガイド

### 廃止されるコンパイラオプション

- **`--target es5`**: ES2015 以上への移行が必須
- **`--moduleResolution node`（node10）**: `nodenext` または `bundler` へ移行
- **`--module amd/umd/systemjs/none`**: ESM への移行が必須
- **`--baseUrl`**: `paths` 内に明示的プレフィックスを含める方式に変更
- **`--moduleResolution classic`**: 完全削除
- **`--outFile`**: 外部バンドラーの使用を推奨
- **`--esModuleInterop false`**: 常に有効化（`false` が廃止）
- **`--downlevelIteration`**: ES5 廃止に伴い不要に

### 言語構文の廃止

- `module` キーワード（名前空間用）→ `namespace` に統一
- import assertions（`asserts`）→ `with` キーワードに変更
- `/// <reference no-default-lib="true"/>` ディレクティブ

### 移行手順

1. TypeScript 6.0 にアップグレード
2. 非推奨警告を確認し、`tsconfig.json` を更新
3. 一時的に `"ignoreDeprecations": "6.0"` で警告を抑制可能（7.0 では無効）
4. `--stableTypeOrdering` フラグで 7.0 との型順序の差異を事前検証

## 今後の注目点

- **TypeScript 7.0**: Go ネイティブ実装で「数ヶ月以内にリリース」と予告。大幅なコンパイル速度向上が期待される
- 6.0 で非推奨のオプションは 7.0 で **完全削除** されるため、6.0 の段階での対応が重要
- 7.0 ではマルチスレッド対応により、大規模プロジェクトでの型チェック速度が劇的に改善される見込み
