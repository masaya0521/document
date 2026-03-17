# TypeScript 6.0 — JavaScript ベース最後のリリースと Go 移行への布石

- **日付**: 2026-03-17（GA リリース）
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [InfoWorld](https://www.infoworld.com/article/4143186/typescript-6-0-reaches-release-candidate-stage.html)

## 概要

TypeScript 6.0 は、現行の JavaScript ベースコンパイラにおける最後のメジャーリリース。Microsoft は「Project Corsa」として Go 言語によるコンパイラ書き換えを進めており、次の TypeScript 7.0 からはネイティブコードベースに移行する。6.0 では `strict: true` のデフォルト化をはじめ、モダン JavaScript に合わせたデフォルト値の大幅変更が行われた。

## 主な変更点

### デフォルト値の刷新

TypeScript 6.0 では、長年のデフォルト設定がモダンな値に更新された:

| オプション | 旧デフォルト | 新デフォルト |
|-----------|-------------|-------------|
| `strict` | `false` | **`true`** |
| `module` | `commonjs` | **`esnext`** |
| `target` | `es3` | **`es2025`** |
| `types` | （全 `@types` パッケージ） | **`[]`**（空配列） |
| `rootDir` | （推論） | **`.`**（tsconfig.json のディレクトリ） |

### 新しい標準ライブラリ機能

- **Temporal API 型**: Stage 3 の Temporal プロポーザルに対応した型定義
- **Map/WeakMap upsert メソッド**: `getOrInsert`、`getOrInsertComputed`
- **`RegExp.escape()`**: Stage 4 到達した正規表現文字のエスケープ関数
- **ES2025 ターゲット**: 新しいビルトイン API 型のサポート

### 型推論の改善

- 明示的な `this` を使用しない関数のコンテキスト感度が低下し、ジェネリック呼び出しでの型パラメータ推論が向上
- オブジェクトリテラルのメソッド構文での推論改善

### Subpath Imports サポート

Node.js の subpath imports で `#/` プレフィックスをサポート。追加のセグメントなしでモジュールエイリアスが設定可能に。

### DOM ライブラリの統合

`dom` lib に `dom.iterable` と `dom.asynciterable` の内容がデフォルトで含まれるようになり、設定が簡素化。

## 破壊的変更・移行ガイド

### 非推奨化されたオプション

以下のオプション・機能が非推奨に:

- `target: es5`
- `--baseUrl`（パスマッピング用途）
- `--moduleResolution node`（`node16` / `nodenext` / `bundler` を推奨）
- AMD / UMD モジュール形式
- レガシーな `module` 名前空間構文

### 移行のポイント

1. **`strict: true` がデフォルトに**: 既存プロジェクトで `strict: false` 前提のコードは明示的に `"strict": false` を `tsconfig.json` に追加する必要あり
2. **`module: esnext` がデフォルトに**: CommonJS 前提のプロジェクトは `"module": "commonjs"` を明示
3. **`types: []` がデフォルトに**: `@types` パッケージの自動読み込みが停止。必要な型を明示的に指定

```jsonc
// tsconfig.json — 既存プロジェクトで 5.x 互換を維持する例
{
  "compilerOptions": {
    "strict": false,        // 5.x のデフォルトを維持
    "module": "commonjs",   // CommonJS プロジェクト向け
    "target": "es2020"      // 必要に応じて調整
  }
}
```

## 今後の注目点

- **TypeScript 7.0（Go ベース）** のリリース時期。Microsoft は「6.0 の直後に続く」と表明しているが、具体的な日程は未発表
- Go ベースコンパイラへの移行による型チェック速度の劇的改善（10 倍以上と見込まれる）
- エコシステム（ESLint、Prettier、IDE プラグイン等）の TypeScript 7.0 対応状況
- `strict: true` デフォルト化に伴う既存プロジェクトの移行コスト
