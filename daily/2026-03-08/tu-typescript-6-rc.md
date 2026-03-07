# TypeScript 6.0 RC — JavaScript ベース最後のリリースと Go ベース TypeScript 7.0 への移行

- **日付**: 2026-03-08
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [InfoQ](https://www.infoq.com/news/2026/02/typescript-6-released-beta/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/03/06/typescript-6-0-rc-bridges-to-go-based-future.aspx)

## 概要

TypeScript 6.0 RC が 2026年3月6日にリリースされた。これは **JavaScript ベースの TypeScript コンパイラとしての最後のリリース** であり、Go で書き直される TypeScript 7.0 への移行を橋渡しする重要なマイルストーンとなる。6.0 では多くのデフォルト値が現代的な設定に変更され、廃止予定の機能が明確化された。

## 主な新機能

### `this` なし関数の文脈感度低減
メソッド構文で書かれた関数でも、`this` が使用されていない場合は型推論が改善され、アロー関数と同様に動作するようになった。

### サブパスインポート（`#/` 構文）
Node.js の最新アップデートに対応し、`"#/*": "./dist/*"` のようなシンプルなマッピングが可能に。

### ES2025 サポート
新しい `es2025` ターゲットで `RegExp.escape` や `Promise.try` などの最新 API をサポート。

### Temporal API 対応
ステージ3の日時 API 提案に対する組み込み型が追加された。

### Map/WeakMap の「アップサート」メソッド
`getOrInsert` と `getOrInsertComputed` メソッドが追加され、デフォルト値の取得・設定が簡潔に。

## 破壊的変更・移行ガイド

### デフォルト値の変更

| オプション | 旧デフォルト | 新デフォルト | 影響 |
|-----------|------------|------------|------|
| `strict` | `false` | `true` | より厳格な型チェック |
| `module` | `commonjs` | `esnext` | ESM が標準に |
| `target` | `es2020` | `es2025` | 最新 JavaScript 対応 |
| `types` | すべての `@types` | 空配列 | ビルド時間 20〜50% 短縮 |

### 廃止されるコンパイラオプション

- `target: es5` → ES2015 以上が必須
- `moduleResolution: node` → `nodenext` または `bundler` へ
- `baseUrl` → `paths` を直接使用
- `moduleResolution: classic` → 削除
- `--outFile` → 外部バンドラー推奨
- `amd`, `umd`, `systemjs` モジュール形式 → 削除

### 廃止される言語機能

- `module Foo {}` 構文 → `namespace Foo {}` を使用
- import assertions (`asserts`) → import attributes (`with`) へ変更
- `alwaysStrict: false` → 常にストリクトモード

### 移行手順

1. **移行支援ツールの利用**: `ts5to6` を使用して自動修正が可能
2. **型エラーが増加する場合**: `types` フィールドに必要な型定義を明示的に指定

```json
{
  "compilerOptions": {
    "types": ["node", "jest"]
  }
}
```

3. **一時的な互換性維持**: 廃止された機能は `"ignoreDeprecations": "6.0"` で一時的に無効化可能（ただし TypeScript 7.0 で完全削除予定）

## 今後の注目点

- **TypeScript 7.0**: Go で書き直されたネイティブコンパイラ。パラレル型チェックにより大幅な速度向上を実現予定
- **TypeScript 6.0 の安定版リリース**: RC から間もなく GA リリース予定（2026年3月17日頃）
- **`ignoreDeprecations: "6.0"` の期限**: TypeScript 7.0 で廃止オプションは完全に削除されるため、早期の移行が推奨される
- **エディタサポート**: Visual Studio 2026 Insiders では TypeScript 7.0 のネイティブプレビューが既に利用可能
