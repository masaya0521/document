# Node.js 26 リリース

- **日付**: 2026-05-14
- **カテゴリ**: Backend / Language Runtime
- **ソース**:
  - [Node.js 26.0.0 (Current) 公式アナウンス](https://nodejs.org/en/blog/release/v26.0.0)
  - [Node.js: Evolving the Node.js Release Schedule](https://nodejs.org/en/blog/announcements/evolving-the-nodejs-release-schedule)
  - [NodeSource: Node.js v26 Is Here](https://nodesource.com/blog/nodejs-v26-is-here)
  - [Help Net Security: Node.js 26 ships with Temporal API enabled by default](https://www.helpnetsecurity.com/2026/05/07/node-js-26-released/)
  - [linuxiac: Node.js 26 Debuts with Temporal API Enabled by Default](https://linuxiac.com/node-js-26-debuts-with-temporal-api-enabled-by-default/)

## 概要

Node.js 26.0.0 が 5/5 にリリースされ、続いて 5/6 に 26.1.0 が出た。V8 14.6 への更新、**Temporal API のデフォルト有効化**、長く非推奨だった内部 stream / HTTP API の削除、Readable ストリームの読み出し挙動の変更が目玉。10 月に LTS 化される予定の "Current" 系列で、今のうちにアプリ側を慣らしておくのに適したタイミング。

実務上のインパクトが大きいのは「Temporal がフラグなしで使える」「内部 `_stream_*` モジュールが完全に削除」「`http.Server.prototype.writeHeader` の削除」「Readable ストリームの read 挙動変更」あたりで、依存ライブラリ側が古い内部 API を掴んでいるとアップデート時に壊れる可能性がある。

## 主な変更点

### Temporal API のデフォルト有効化

ECMAScript Temporal proposal の API が **フラグなしで使える**ようになった。`Temporal.Now`、`Temporal.PlainDate`、`Temporal.ZonedDateTime` などが直接呼べる。

```js
const now = Temporal.Now.zonedDateTimeISO('Asia/Tokyo');
const tomorrow = now.add({ days: 1 });
console.log(tomorrow.toString());
```

`Date` 由来の罠（タイムゾーン、ミリ秒精度、ローカルタイムの曖昧さ）を回避する手段が、ライブラリ依存なしで手に入ったのが大きい。

### V8 14.6 で増えるビルトイン

V8 が 14.6.202.33（Chromium 134 相当）に上がる。主な追加 API は以下。

- `Map.prototype.getOrInsert(key, defaultValue)` / `WeakMap.prototype.getOrInsert(...)`
- `Map.prototype.getOrInsertComputed(key, callback)` / `WeakMap.prototype.getOrInsertComputed(...)`
- `Iterator.concat(...)` — 複数 iterator を順に消費するヘルパ

```js
const counts = new Map();
for (const word of words) {
  counts.set(word, counts.getOrInsertComputed(word, () => 0) + 1);
}
```

### Undici / fetch

Undici 8 が同梱され、`fetch()` 経由の HTTP 挙動が更新される。HTTP/2 周りも継続的に強化。

### Readable streams の読み出し挙動変更

Readable streams が **read-ahead を行わず、1 バッファずつ読む** ように変わった。背圧（backpressure）の効きが変わるので、自前で stream を `read()` ループで叩いている実装はメモリ・スループット挙動が変わる可能性がある。

## 破壊的変更・移行ガイド

特に効くのは以下。

- **削除された内部 stream モジュール**: `_stream_wrap` / `_stream_readable` / `_stream_writable` / `_stream_duplex` / `_stream_transform` / `_stream_passthrough` は **完全に削除**。古い `require('_stream_readable')` のような呼び出しを残しているライブラリは即時に落ちる。
- **`http.Server.prototype.writeHeader()` 削除**: `writeHead()` を使う。
- **`module.register()` がランタイム deprecate**: ローダーフックを使っているコードは将来削除の前提で対応を進める。
- **`--experimental-transform-types` フラグ削除**: TS の inline 変換に頼った起動シーケンスは別経路（`tsx`、`ts-node`、ビルド済み JS）に寄せる。
- **Readable streams の read 挙動変更**: 上述の通り。`stream.pipeline()` を使っている分には影響は小さいが、`read()` を直接ポーリングしている実装は要検証。

移行手順としては、(1) 依存ライブラリの Node.js 26 対応バージョンへ更新、(2) `--throw-deprecation` を付けた CI ジョブで `module.register()` などの実行時 deprecation を炙り出す、(3) 削除済み API への参照を grep で潰す、の順が現実的。

## 今後の注目点

- **10 月の LTS 移行**: 26.x が 2026 年 10 月に LTS 化される予定。LTS 移行前に「依存が 26 で動く」「Temporal を取り込めるところは取り込む」状態を作っておけると、LTS 採用判断が早く取れる。
- **Temporal の浸透**: ライブラリ側（date-fns / Luxon / dayjs 系）が Temporal をネイティブに扱う API を整えていくフェーズに入る。新規コードは早めに `Date` を Temporal に置き換える方針が取りやすくなる。
- **Bun / Deno との Web 標準競争**: Bun 1.3.x が HTTP/2・HTTP/3 を試験投入、Deno も Temporal を以前から積んでいる。Node.js 26 で標準化が揃ったことで、ランタイム間の API 互換性は今後数か月でかなり収束しそう。
