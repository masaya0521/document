# TypeScript 6.0 Beta — JavaScript ベース最後のリリースと Go ベース 7.0 への道

- **日付**: 2026-02-18
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/), [InfoWorld](https://www.infoworld.com/article/4131798/last-javascript-based-typescript-arrives-in-beta.html)

## 概要

TypeScript 6.0 Beta が 2026年2月11日に発表された。これは **JavaScript ベースで開発される最後の TypeScript リリース** であり、次の 7.0 からは Go で書き直されたコンパイラに移行する。6.0 では多数のデフォルト設定変更と破壊的変更が含まれ、モダンな開発環境を前提とした大胆な簡素化が行われている。

RC は 2/24、正式版は 3/17 にリリース予定。インストールは `npm install -D typescript@beta` で可能。

## 主な変更点

### 新機能

**コンテキスト感度の改善**: `this` を使用しない関数のコンテキスト感度が改善され、オブジェクトプロパティの宣言順序に関係なく型パラメータの推論が正しく動作するようになった。

**Subpath Import サポート**: Node.js の `#/` プレフィックスによるパッケージ内部インポートをサポート。`node20`, `nodenext`, `bundler` モジュール解決設定で利用可能。

**新しい JavaScript API 型**:
- **Temporal**: Stage 3 のプロポーザルに対応した日付・時刻操作の標準型
- **RegExp.escape**: 正規表現のエスケープ
- **Map/WeakMap upsert メソッド**: `getOrInsert`, `getOrInsertComputed`

**DOM 改善**: `dom.iterable` が `dom` ライブラリにデフォルト包含されるようになり、別途参照が不要に。

### デフォルト設定の変更

| 設定 | 旧デフォルト | 新デフォルト |
|------|-------------|-------------|
| `strict` | `false` | **`true`** |
| `module` | `commonjs` | **`esnext`** |
| `target` | ― | **当年の ES バージョン (`es2025`)** |
| `types` | 全 `@types` パッケージ自動列挙 | **`[]`（空配列）** |
| `rootDir` | 推論 | **tsconfig ディレクトリ** |

## 破壊的変更・移行ガイド

以下のオプションは非推奨となり、`"ignoreDeprecations": "6.0"` を設定しない限りエラーになる：

| 削除/非推奨 | 代替手段 |
|------------|---------|
| ES5 ターゲット | ES2015 以上を使用 |
| AMD, UMD, SystemJS モジュール形式 | ESM に移行 |
| `baseUrl` オプション | `paths` で相対パスを使用 |
| Classic モジュール解決 | `node`, `nodenext`, `bundler` を使用 |
| `--outFile` | 外部バンドラ（Vite, esbuild 等）を使用 |
| レガシー `module` キーワード（名前空間用） | `namespace` キーワードを使用 |
| `esModuleInterop: false` | `esModuleInterop: true`（デフォルト）を使用 |

### 移行のポイント

1. **`strict: true` がデフォルト**: 既に `strict: true` を明示している場合は影響なし。そうでない場合は型エラーが増える可能性あり
2. **`module: esnext` がデフォルト**: CommonJS に依存している場合は明示的に `"module": "commonjs"` を設定
3. **`types: []` がデフォルト**: グローバル型定義に依存している場合は明示的に `types` を指定

### TypeScript 7.0 への準備

`--stableTypeOrdering` フラグが追加された。これは 6.0 と今後の Go ベース 7.0 の間の差異を検出するためのもの。7.0 では内部アーキテクチャが根本的に変わるが言語互換性は維持される。このフラグを有効にして 6.0 での出力を安定させておくと、7.0 への移行がスムーズになる。

## 今後の注目点

- **TypeScript 7.0（2026年中〜後半予定）**: Go ベースのコンパイラにより 5-10倍の高速化、エディタ起動時間約8倍改善、メモリ使用量約50%削減が見込まれる
- **エコシステムへの影響**: ES5 ターゲットや CommonJS デフォルトの廃止により、レガシープロジェクトは明示的な設定追加が必要。新規プロジェクトはよりシンプルな tsconfig で開始可能に
- **Temporal API の普及**: TypeScript が Temporal 型をネイティブサポートしたことで、日付処理ライブラリ（moment, date-fns, dayjs 等）からの移行が加速する可能性
