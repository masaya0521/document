# TypeScript 6.0 — JS ベース最終リリースと v7.0 への移行

- **日付**: 2026-03-23
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [RC 発表](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/)

## 概要

TypeScript 6.0 は、現行の JavaScript ベースコンパイラとしての**最終メジャーリリース**。Go で書き直された TypeScript 7.0（コードネーム "Corsa"）への橋渡しとして位置づけられており、デフォルト値の刷新とレガシーオプションの廃止を通じて、移行の準備を促す内容となっている。

機能面では Temporal API のネイティブサポートが最大の目玉で、JavaScript の長年の課題であった日付/時刻処理が型安全に行えるようになった。

## 主な変更点

### 新機能

- **Temporal API サポート**: Stage 4 に到達した Temporal 提案のビルトイン型定義を追加。イミュータブルな日時操作、タイムゾーン対応、暦システム、ナノ秒精度を型安全に利用可能
- **`RegExp.escape`**: 正規表現文字のエスケープ関数（Stage 4 提案）
- **Map/WeakMap `getOrInsert`**: ECMAScript "upsert" 提案（Stage 4）に基づく新メソッド
- **`es2025` ターゲット**: 新しいコンパイルターゲットとして追加
- **`this` を使用しない関数の型推論改善**: メソッド構文でのコンテキスト依存性を削減
- **サブパスインポート**: `#/` で始まる Node.js サブパスインポートのサポート

### デフォルト値の変更

| オプション | 旧デフォルト | 新デフォルト |
|-----------|------------|------------|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | `es3` | `es2025` |
| `types` | （全ての `@types` を自動取得） | `[]`（空配列） |
| `rootDir` | （推論） | tsconfig.json のディレクトリ |

### 廃止予定（v7.0 で削除）

- `target: es5` — 最古のターゲットは ES2015 に
- `--baseUrl` — パスマッピングには明示的プレフィックスを使用
- `--moduleResolution node` / `classic`
- `amd`、`umd`、`systemjs` モジュール形式
- `--outFile`
- `--downlevelIteration`

## 破壊的変更・移行ガイド

### `types` のデフォルト変更への対応

最も影響が大きい変更。`@types/node` などが自動的に読み込まれなくなるため、明示的な指定が必要:

```json
{
  "compilerOptions": {
    "types": ["node"]
  }
}
```

旧動作に戻す場合は `"types": ["*"]` を指定。

### `baseUrl` 廃止への対応

パスマッピングに明示的なプレフィックスを記述:

```json
{
  "compilerOptions": {
    "paths": {
      "@app/*": ["./src/app/*"]
    }
  }
}
```

### `strict: true` のデフォルト化

既存プロジェクトで strict mode を使っていない場合、明示的に `"strict": false` を設定する必要がある。ただし、これを機に strict mode への移行を検討することが推奨されている。

## 今後の注目点

- **TypeScript 7.0（Corsa）**: Go ベースの新コンパイラ。数カ月以内のリリースを予定
  - コンパイル速度 5-10x 向上
  - インクリメンタルビルドがほぼ即時に
  - エディタ起動が約 8x 高速化
  - メモリ使用量が約 50% 削減
- 6.0 で廃止予定となったオプションの完全削除
- Temporal API の各ランタイム（Node.js、Deno、ブラウザ）での実装進捗
