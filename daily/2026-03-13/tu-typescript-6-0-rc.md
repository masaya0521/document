# TypeScript 6.0 RC — Go ベースの未来への架け橋

- **日付**: 2026-03-13
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [InfoWorld](https://www.infoworld.com/article/4143186/typescript-6-0-reaches-release-candidate-stage.html)

## 概要

TypeScript 6.0 RC が 2026年3月6日にリリースされた。GA は 3月17日を予定。本リリースは **JavaScript ベースの最終メジャーバージョン** であり、Go で再実装される TypeScript 7.0（コードネーム "Corsa"）への移行を見据えた戦略的リリースとなっている。

7.0 では 5〜10 倍のコンパイル速度向上、約 8 倍のエディタ起動改善、約 50% のメモリ削減が期待されており、6.0 はそのための互換性橋渡しの役割を担う。

## 主な変更点

### 新機能

- **`es2025` ターゲット追加**: `RegExp.escape()` や Temporal API の型定義を含む
- **Map の `getOrInsert()` / `getOrInsertComputed()`**: キー存在確認の冗長な記述が不要に
- **サブパス import の `#/` サポート**: Node.js の `#/` プレフィックスに対応、パスマッピングを簡潔化
- **`this` なし関数の推論改善**: メソッド構文とアロー関数構文の推論結果の差異を解消

### デフォルト値の変更

| 設定 | 旧デフォルト | 新デフォルト |
|------|-------------|-------------|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | 固定値 | `es2025`（浮動的最新版） |
| `types` | 自動列挙 | `[]`（明示指定が必要） |

### 削除されたオプション

- `--target es5`
- `--outFile`
- `--moduleResolution node`（node10）
- `--module amd/umd/systemjs`
- `--baseUrl`

## 破壊的変更・移行ガイド

### 必須対応

1. **`types` の明示指定**: `tsconfig.json` で `"types": ["node"]` 等を明示的に指定する必要がある。自動列挙が無効になったため、型定義パッケージが見つからないエラーが発生する可能性がある
2. **`module` の確認**: デフォルトが `esnext` に変わるため、CommonJS プロジェクトでは明示的に `"module": "commonjs"` を指定する
3. **ES5 ターゲットの廃止**: ES5 をサポートする必要があるプロジェクトは 5.x 系に留まる必要がある

### 移行支援

- `--stableTypeOrdering` フラグで型出力順序を 7.0 仕様に合わせられる（パフォーマンスへの影響あり）
- `"ignoreDeprecations": "6.0"` で非推奨警告を一時的に抑制可能（7.0 では無効）
- デフォルト変更の影響でビルド時間が 20〜50% 改善される傾向あり

## 今後の注目点

- **TypeScript 7.0（Corsa）**: Go ベースの新コンパイラ。2026年中盤〜後半のリリースを予定
- 7.0 では共有メモリ・マルチスレッドを活用し、大規模プロジェクトでのコンパイル体験が劇的に改善される見込み
- 6.0 で非推奨となった機能は 7.0 で完全に削除されるため、早期の移行対応が推奨される
