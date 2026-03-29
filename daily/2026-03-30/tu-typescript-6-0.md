# TypeScript 6.0 — Go ネイティブ 7.0 への橋渡しリリース

- **日付**: 2026-03-23
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/03/23/typescript-6-0-ships-as-final-javascript-based-release-clears-path-for-go-native-7-0.aspx)

## 概要

TypeScript 6.0 は JavaScript ベースで実装された最後の TypeScript リリース。次期 TypeScript 7.0（Project Corsa）は Go 言語でネイティブ実装され、マルチスレッド対応により 7〜10x のコンパイル高速化を実現する。6.0 はその橋渡しとして、多数のデフォルト値変更・オプション非推奨化を行い、開発者に移行準備を促すリリースとなっている。

## 主な変更点

### 新機能

- **Temporal API** の組み込み型サポート
- **`Map.getOrInsert`** / **`WeakMap.getOrInsert`** メソッドの型定義
- **`RegExp.escape`** 関数の型定義
- **サブパスインポート拡張**: `#/*` で始まるシンプルなサブパスインポート対応
- **`dom.iterable`/`dom.asynciterable`** を `dom` に統合（設定の簡素化）
- **`this` 推論改善**: 未使用の `this` をコンテキスト依存性判定から除外

### `--stableTypeOrdering` フラグ

6.0 と 7.0 間での型の順序付けの違いを診断するための一時フラグ。最大 25% のパフォーマンス低下があるため診断目的限定。

## 破壊的変更・移行ガイド

### デフォルト値の変更

| オプション | 旧デフォルト | 新デフォルト |
|---|---|---|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | `es3` | `es2025` |
| `types` | （全型定義を自動包含） | `[]`（空配列） |
| `rootDir` | （推論） | `tsconfig.json` の親ディレクトリ |

### 非推奨化されるオプション

以下のオプションは 6.0 で非推奨警告、7.0 で完全削除される:

- `--target es5`
- `--moduleResolution node` / `classic`
- `--module amd` / `umd` / `systemjs`
- `--baseUrl`
- `--outFile`
- `esModuleInterop: false`
- `allowSyntheticDefaultImports: false`

### 言語機能の非推奨化

- `import assertions`（`assert` キーワード → `with` キーワードへ移行）
- `module` キーワード（`namespace` へ移行）
- `/// <reference no-default-lib="true"/>`

### 移行手順

```jsonc
// tsconfig.json — 非推奨警告を一時的に抑止
{
  "compilerOptions": {
    "ignoreDeprecations": "6.0",
    // 以下を明示的に指定する
    "types": ["node"],
    "rootDir": "./src"
  }
}
```

`"ignoreDeprecations": "6.0"` で警告を抑止できるが、TypeScript 7.0 では廃止オプション自体が削除されるため、早期の対応が推奨される。

## 今後の注目点

- **TypeScript 7.0 正式リリース時期**: Go ネイティブ実装。2026 年前半に安定版が見込まれる
- **`tsgo` コマンド**: TypeScript 7.0 の新コンパイラ。既に試験利用可能
- **エコシステムの対応状況**: ESLint、Prettier、各種フレームワークの TypeScript 7.0 対応
- **`baseUrl` 廃止の影響**: モノレポ構成での `paths` 設定の見直しが必要
