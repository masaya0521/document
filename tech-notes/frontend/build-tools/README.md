# フロントエンドビルドツールの全体像

JavaScript のモジュールシステムの歴史から、現代のビルドツール（Vite, Rollup, esbuild, Rolldown）までを整理する。

## 1. JavaScript モジュールシステムの歴史

初期の JavaScript にはモジュールの仕組みが存在せず、すべてがグローバルスコープに置かれていた。

```html
<!-- 昔のやり方：スクリプトの読み込み順序に依存 -->
<script src="jquery.js"></script>
<script src="utils.js"></script>
<script src="app.js"></script>
```

この方式には名前衝突、依存関係の不明確さ、読み込み順序への依存という問題があった。

### モジュールシステムの変遷

| 時期 | 仕様 | 環境 |
|---|---|---|
| 2009年 | **CommonJS** (`require`/`module.exports`) | Node.js |
| 2011年 | **AMD** (`define`/`require`) | ブラウザ（RequireJS） |
| **2015年** | **ES Modules** (`import`/`export`) | **ECMAScript 言語仕様として標準化** |

CommonJS や AMD はコミュニティが作った非公式な仕様。ES Modules は ECMAScript に正式に組み込まれた公式のモジュールシステム。

## 2. ES Modules（ESM）

```js
// math.js — エクスポート
export function add(a, b) {
  return a + b
}

// app.js — インポート
import { add } from './math.js'
console.log(add(1, 2)) // 3
```

### ESM の特徴

- **静的解析が可能** — `import`/`export` はファイルの先頭に書く必要があり、実行前に依存関係が確定する。これにより Tree Shaking（未使用コードの除去）が可能
- **非同期読み込み** — ブラウザがモジュールを非同期で取得できる
- **スコープが独立** — 各モジュールは独自のスコープを持ち、明示的に export したものだけが外部から参照可能

## 3. CommonJS の制約

Node.js のサーバーサイド用途としてはうまく機能したが、以下の制約がある。

### 動的な require

```js
const mod = require(condition ? './foo' : './bar')
const lib = require(`./plugins/${name}`)
```

`require` は普通の関数なので変数や条件分岐の中で自由に使える。柔軟だが、実行するまでどのモジュールを読み込むか分からないため：

- **Tree Shaking ができない** — 使われていないコードを事前に判別できず、バンドルサイズが大きくなる
- **静的解析ツールが困る** — エディタの補完やリンターが依存関係を正確に把握できない

### 同期読み込み

```js
const data = require('./heavy-module') // ここで処理がブロックされる
```

Node.js ではファイルシステムから読むだけなので問題になりにくいが、ブラウザではネットワーク越しに取得する必要がある。同期読み込みはブラウザの描画をブロックしてしまうため、CommonJS はブラウザで直接動かせない。

### exports の挙動が分かりにくい

```js
// これは動く
exports.foo = 'bar'

// これは動かない（参照が切れる）
exports = { foo: 'bar' }

// こう書く必要がある
module.exports = { foo: 'bar' }
```

`exports` は `module.exports` への参照に過ぎないため、再代入すると壊れる。

## 4. バンドラーの系譜

### Webpack（2012年〜）

CommonJS 時代に生まれたバンドラー。各モジュールを関数でラップし、独自のランタイムで結合する方式。

- 開発サーバー起動時に全モジュールの依存関係を解析し、全体をバンドルしてからブラウザに配信
- CSS・画像など非 JS アセットの処理も標準で豊富
- プロジェクトが大きくなるほど起動・ビルドが遅くなる

### Rollup（2015年〜）

Rich Harris（Svelte の作者）が開発。ES Modules を前提に設計されたバンドラー。

```js
// src/utils.js
export function add(a, b) { return a + b }
export function sub(a, b) { return a - b }  // 未使用

// src/app.js
import { add } from './utils.js'
console.log(add(1, 2))
```

Rollup の出力（フラットに結合、未使用の sub は消える）：

```js
function add(a, b) { return a + b }
console.log(add(1, 2))
```

Webpack の出力（モジュールごとに関数でラップされ、ランタイムが付く）：

```js
(function(modules) {
  // webpack ランタイム...
})({
  './utils.js': function(exports) { ... },
  './app.js': function(exports) { ... }
})
```

| | Rollup | Webpack |
|---|---|---|
| Tree Shaking | 優秀（設計の根幹） | 後から対応、Rollup ほど徹底されていない |
| 出力サイズ | 小さい | ランタイム分だけ大きい |
| ライブラリのビルド | 得意 | やや冗長 |
| 開発サーバー・HMR | 自前では持たない | 充実 |

React や Vue など多くの OSS ライブラリが Rollup でビルドされている。

### esbuild（2020年〜）

Evan Wallace（Figma の共同創業者）が開発。Go 製のバンドラー・トランスパイラ。

- JavaScript/TypeScript のバンドル・トランスパイル・ミニファイを高速に行う
- **型チェックをしない**。TypeScript の構文を理解して除去するだけ

```ts
// esbuild はこの型注釈を単に消すだけ
const x: number = 1  →  const x = 1
```

### Rolldown（開発中）

Vite チーム（Evan You が主導）が開発。Rust 製の Rollup 後継。

- Rollup 互換 API でプラグインエコシステムをそのまま活かせる
- トランスパイルも内蔵（内部で oxc を使用）し、esbuild の役割も兼ねる
- Vite の次期バンドラーとして、Vite 7 での統合が見込まれている

## 5. Vite

Evan You（Vue.js の作者）が開発したフロントエンド開発用のビルドツール。

### アーキテクチャ

**開発時（ネイティブ ESM 方式）：**

1. 開発サーバー起動時にはバンドルしない
2. ブラウザが `<script type="module">` で直接 `import` 文を解釈
3. ブラウザがモジュールを要求した時点で、そのファイルだけを変換・配信（esbuild で変換）

→ 起動時のコストがほぼゼロ。プロジェクト規模に依存しにくい高速 HMR。

**本番ビルド：**

Rollup でバンドル。ネイティブ ESM をそのまま本番で使うと HTTP リクエスト数が膨大になりパフォーマンスが悪化するため。

### Webpack との比較

| | Webpack | Vite |
|---|---|---|
| 開発サーバー起動 | 遅い（全体バンドル） | 速い（オンデマンド） |
| HMR | プロジェクト規模に比例して遅くなる | 規模に依存しにくい |
| 設定 | 複雑になりがち | シンプル |

### 現在と将来

```
Vite 現在:  esbuild（開発時変換） + Rollup（本番バンドル）
Vite 将来:  Rolldown（両方を統一）
```

現在の Vite は開発と本番で異なるツールを使うため、微妙に挙動が異なるケースがある。Rolldown で統一されれば一貫性が向上し、ビルドもさらに高速化される。

## 6. tsgo — TypeScript コンパイラの Go 実装

Microsoft の TypeScript チーム公式による、`tsc` の Go ネイティブ実装。大規模プロジェクトでの型チェックを10倍程度高速化することを目指している。

### esbuild との違い

| | esbuild | tsgo |
|---|---|---|
| 言語 | Go | Go |
| 役割 | バンドラー・トランスパイラ | 型チェッカー |
| TypeScript の型を検査するか | **しない** | **する（本業）** |
| 出力 | バンドルされた JS ファイル | 型エラーの報告、`.d.ts` 生成 |
| 置き換え対象 | Webpack, Rollup など | `tsc` |

esbuild が速いのは「型チェックを捨てた」から。tsgo は「型チェックそのものを速くする」アプローチ。両者は補完関係にあり、競合するものではない。

```
エディタ上の型チェック  →  tsc（将来は tsgo）
ビルド・バンドル        →  esbuild / Vite / Rollup
```
