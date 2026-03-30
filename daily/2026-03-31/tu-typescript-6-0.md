# TypeScript 6.0 — JavaScript ベース最後のメジャーリリースと 7.0 移行ガイド

- **日付**: 2026-03-31
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/03/23/typescript-6-0-ships-as-final-javascript-based-release-clears-path-for-go-native-7-0.aspx)

## 概要

TypeScript 6.0 は 2026年3月23日にリリースされた、JavaScript ベースのコンパイラとしては最後のメジャーバージョンである。Go 言語で再実装された TypeScript 7.0（Project Corsa）への移行を支援するブリッジリリースとして位置づけられており、多数のデフォルト値変更と非推奨化が含まれる。

TypeScript 7.0 はフルビルドで約 10 倍の高速化を実現しており、数ヶ月以内のリリースが予定されている。6.0 で非推奨となった機能は 7.0 で完全に削除されるため、早期の対応が推奨される。

## 主な新機能

### 型推論の改善
- `this` を使用しない関数でメソッド構文と矢印関数の型推論が統一
- プロパティ順序に依存しない一貫した推論

### モジュール解決の拡張
- `#/` サブパスインポート対応（Node.js 20 最新版との整合性）
- `--moduleResolution bundler` と `--module commonjs` の組み合わせが可能に

### 新しい ECMAScript 機能対応
- **Temporal API**（ステージ 4）: `Temporal.Now.instant().subtract({ hours: 24 })`
- **Map/WeakMap の upsert メソッド**: `map.getOrInsert("key", defaultValue)`
- **RegExp.escape**（ステージ 4）: 正規表現特殊文字の安全なエスケープ

### その他
- `lib.dom.iterable` と `lib.dom.asynciterable` が `lib.dom` に統合
- `es2025` ターゲットの追加

## 破壊的変更・移行ガイド

### デフォルト値の重要な変更

| 設定 | 旧デフォルト | 新デフォルト |
|------|-----------|-----------|
| `strict` | `false` | **`true`** |
| `module` | `commonjs` | **`esnext`** |
| `target` | `es2020` | **`es2025`** |
| `types` | すべて列挙 | **`[]`（空配列）** |
| `rootDir` | 推論 | **`.`（tsconfig.json の親ディレクトリ）** |

### TypeScript 7.0 で削除される非推奨機能

**ターゲット関連:**
- `target: es5` — ES2015 以上への移行が必須
- `--downlevelIteration` — ES5 出力廃止に伴い不要

**モジュール解決:**
- `--moduleResolution node/node10` — `nodenext` または `bundler` に移行
- `--moduleResolution classic` — 完全削除

**モジュール形式:**
- `amd`, `umd`, `systemjs`, `none` の `--module` 値 — ESM 推奨

**その他:**
- `--baseUrl` — `paths` でプレフィックスを明示指定
- `--outFile` — 外部バンドラーの使用を推奨
- `esModuleInterop: false` — デフォルト有効化
- `module` キーワード（名前空間構文）— `namespace` に変更

### 移行手順

1. **TypeScript 6.0 にアップグレード**
2. **非推奨警告を確認** — ビルド時に表示される警告を一つずつ対応
3. **`types` フィールドを明示設定** — 特に `"types": ["node"]` 等
4. **`rootDir` を明示設定** — `./src` 等
5. **`ts5to6` ツール** — `baseUrl` と `rootDir` の自動調整が可能
6. **一時的な抑制** — `"ignoreDeprecations": "6.0"` で警告を抑制可能（7.0 では無効）
7. **7.0 のプレビュー検証** — `@typescript/native-preview` パッケージで事前テスト

## 今後の注目点

- TypeScript 7.0（Project Corsa）のリリースが数ヶ月以内に予定
- 7.0 ではフルビルド約 10 倍高速化、並列プロジェクトビルド対応
- 既存の Strada API は 7.0 で非サポート — プラグイン・ツールチェーンの互換性確認が必要
- ダウンレベルコンパイルは es2021 までに制限（デコレータ emit 非対応）
