# TypeScript 6.0 破壊的変更まとめ

2026年3月25日に発表された TypeScript 6.0 の破壊的変更について、各オプションの役割と削除理由を整理する。

- 公式ブログ: https://devblogs.microsoft.com/typescript/announcing-typescript-6-0

## 位置づけ

TypeScript 6.0 は Go で書き直された **TypeScript 7.0（ネイティブ版）** への「橋渡しリリース」。7.0 では非推奨機能がすべて削除されるため、6.0 の段階で `"ignoreDeprecations": "6.0"` を活用しつつ段階的に移行することが推奨されている。

## 主要な新機能

| 機能 | 概要 |
|---|---|
| `this` なし関数の型推論改善 | メソッド構文でもアロー関数と同等の型推論が効くように |
| `#/` サブパスインポート | Node.js の `"#/*": "./dist/*"` マッピングに対応 |
| `--stableTypeOrdering` フラグ | 6.0 / 7.0 間の型順序の差異を検出する診断ツール |
| ES2025 サポート | `RegExp.escape()`, `Temporal` API, `Map`/`WeakMap` の upsert メソッド |
| DOM 型の統合 | `lib.dom.iterable` 等が `lib.dom` に統合 |

## デフォルト値の変更

| オプション | 内容 | 旧デフォルト | 新デフォルト |
|---|---|---|---|
| `strict` | 厳密な型チェック群の一括有効化 | `false` | `true` |
| `module` | 出力モジュール形式 | `commonjs` | `esnext` |
| `target` | 出力 JS バージョン | `es2020` | `es2025` |
| `types` | 自動読み込みする `@types/*` | 全部 | `[]`（空） |
| `rootDir` | ソースのルートディレクトリ | 自動推論 | tsconfig.json の親ディレクトリ |

特に **`types` が `[]`** になる変更は影響が大きい。`@types/node` などを明示的に指定しないと型が認識されなくなる。

## 削除されるオプション

### `target: es5`

出力する JavaScript のバージョンを指定するオプション。`es5` は 2009 年の仕様で、以下のような変換（ダウンレベルコンパイル）が行われていた。

- `class` → `function` + `prototype`
- アロー関数 → `function`
- `const` / `let` → `var`

**削除理由:** 現在のブラウザ・Node.js はすべて ES2015+ をネイティブサポートしており、ES5 への変換は不要。変換コードはサイズが増え、デバッグも困難になる。

### `--downlevelIteration`

`for...of`、スプレッド構文（`[...arr]`）、分割代入などのイテレーションを ES5 互換のコードに変換する際、`Symbol.iterator` プロトコルを正しくエミュレートするフラグ。

- `false` — 配列前提の簡易変換
- `true` — 仕様準拠のヘルパーコードを挿入

**削除理由:** `target: es5` の削除に伴い不要に。ES2015+ では言語仕様としてイテレーションプロトコルがネイティブサポートされている。

### `--moduleResolution node` (`node10`)

`import` 文のモジュール解決アルゴリズムを指定するオプション。`node`（`node10`）は Node.js の CommonJS 時代の解決ロジックを再現する。

- 拡張子省略（`./foo` → `./foo.js`）
- `index.js` 探索（`./dir` → `./dir/index.js`）
- `package.json` の `main` フィールド参照

**削除理由:** 現在の Node.js は `exports` フィールドや ESM をサポートしており、`node10` の挙動では正しく解決できないパッケージが増えている。`nodenext`（Node.js 最新仕様準拠）または `bundler`（バンドラー前提）へ移行が必要。

### `--module amd / umd / systemjs / none`

TypeScript が出力するモジュール形式を指定するオプション。

| 値 | 用途 |
|---|---|
| `amd` | RequireJS 用の `define()` 形式。ブラウザ向け非同期モジュール読み込み |
| `umd` | AMD + CommonJS 両対応ラッパー。ライブラリ配布用 |
| `systemjs` | SystemJS ローダー用の `System.register()` 形式 |
| `none` | モジュールシステムなし。グローバルスコープの `<script>` タグ前提 |

**削除理由:** いずれもレガシーなモジュール形式。ESM（ES Modules）がブラウザ・Node.js の標準となり、バンドラーも ESM を前提としている。

### `--baseUrl`

非相対パスのインポート（`import { foo } from 'utils/foo'`）をどのディレクトリを起点に解決するかを指定するオプション。プロジェクトルートを指定すると `../../` のような深い相対パスを避けられる。

**削除理由:** `paths` オプションだけで同等のマッピングが可能。`baseUrl` は副作用として `node_modules` 内のパッケージ解決にも影響を与えるため、意図しないモジュール解決を引き起こすことがあった。

### `--moduleResolution classic`

TypeScript 1.x 時代のモジュール解決アルゴリズム。相対パスはそのまま解決し、非相対パスはソースファイルの位置から親ディレクトリを順に遡って探索する。`node_modules` は参照しない。

**削除理由:** npm エコシステムと互換性がなく、実用上使われていない。

### `--outFile`

複数の TypeScript ファイルを **1つのファイルに結合して出力** するオプション。AMD / SystemJS モジュールとの組み合わせで使われていた。

**削除理由:** バンドリングは webpack / Vite / esbuild 等の専用ツールが担うべき責務。TypeScript 本体のバンドル機能は最適化もコード分割もできず、実用的でなかった。

### `esModuleInterop: false` / `allowSyntheticDefaultImports: false`

CommonJS モジュールを ESM の `import` 構文で読み込む際の互換性オプション。

- **`esModuleInterop`** — `default` エクスポートが存在しない CommonJS モジュールにもデフォルトインポート（`import fs from 'fs'`）を許可するヘルパーコードを挿入する
- **`allowSyntheticDefaultImports`** — 型チェックレベルでのみ上記を許可する（ヘルパーは挿入しない）

**削除理由:** `false` にすると `import * as fs from 'fs'` のような不自然な記法を強いられる。事実上すべてのプロジェクトが `true` で運用しており、`false` は実害しかなかった。6.0 からは常に有効。

### `alwaysStrict: false`

出力する JS ファイルの先頭に `"use strict";` を付けるかどうか。`false` だと非 strict モードで動作する。

**削除理由:** ESM は仕様上常に strict mode。非 strict モードは `with` 文や暗黙のグローバル変数など、現代では使うべきでない機能を許容してしまう。

### レガシー `module` 構文

TypeScript 独自の `module Foo { ... }` 構文。内部モジュール（名前空間）を定義するもので、ES Modules 以前に複数ファイル間でスコープを分割するために使われていた。

**削除理由:** `namespace` キーワードで同じことができる。`module` は ES Modules の `module` と紛らわしいため、長年非推奨だった。

### import assertions (`assert`)

```typescript
// 旧: import assertions（削除）
import data from './data.json' assert { type: 'json' }

// 新: import attributes
import data from './data.json' with { type: 'json' }
```

**削除理由:** TC39 の仕様策定過程で `assert` から `with` に構文が変更された。`with` キーワードを使う import attributes が正式仕様。

## `tsgo` と `tsc` の関係

TypeScript 7.0 のコアエンジンとなる `tsgo`（Go 実装）は `@typescript/native-preview` パッケージで先行提供されている。

| | tsgo | tsc |
|---|---|---|
| 実装言語 | Go | JavaScript (自己ホスティング) |
| 速度 | 約10倍高速 | 従来通り |
| 対応機能 | 型チェック（`--noEmit`）のみ | 型チェック + トランスパイル + エミット |

現時点では `tsgo` は型チェック専用。ビルド時のトランスパイルはバンドラー（Vite / esbuild 等）が担う構成が前提となる。

## tsgo と Vite の役割の違い

`tsgo` が進化しても Vite（またはそれに相当するバンドラー）は引き続き必要。

| 機能 | tsgo | Vite |
|---|---|---|
| 型チェック | 対応 | 非対応 |
| トランスパイル (TS→JS) | 将来対応予定 | 対応（esbuild/SWC 経由） |
| バンドル（複数ファイル→1つにまとめる） | 非対応 | 対応（Rollup/Rolldown 経由） |
| 開発サーバー（HMR 等） | 非対応 | 対応 |
| アセット処理（CSS, 画像等） | 非対応 | 対応 |
