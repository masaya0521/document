# Node.js 26 — Temporal API デフォルト有効化と node:ffi 追加

- **日付**: 2026-05-12
- **カテゴリ**: Backend / Language Runtime
- **ソース**:
  - [Node.js 26.0.0 リリースブログ](https://nodejs.org/en/blog/release/v26.0.0)
  - [Node.js 26.1.0 リリース (GitHub)](https://github.com/nodejs/node/releases/tag/v26.1.0)
  - [CHANGELOG_V26.md](https://github.com/nodejs/node/blob/main/doc/changelogs/CHANGELOG_V26.md)
  - [Help Net Security: Node.js 26 ships with Temporal API enabled by default](https://www.helpnetsecurity.com/2026/05/07/node-js-26-released/)

## 概要

Node.js 26.0.0 が 2026-05-05 に新 Current ラインとしてリリースされ、続いて 26.1.0 が 2026-05-07 に公開された。今リリースの目玉は「`Temporal` API のデフォルト有効化」と「`node:ffi` モジュール（実験的）」の追加で、JavaScript 標準への追従とランタイム機能の拡張が一気に進んだ。Node.js 26 は 2026年10月に LTS へ昇格する予定で、それまでの約 6 ヶ月間が Current として最新機能の検証期間となる。

V8 は 14.6.202.33（Chromium 146 相当）に更新され、HTTP クライアントの Undici は 8.0 に上がっている。同時に古い API の削除や Readable Stream の挙動変更など、いくつかの破壊的変更も含まれる点に注意が必要。

## 主な変更点

### Temporal API のデフォルト有効化

Temporal は `Date` を置き換える次世代の日時 API で、これまでは TC39 Stage 3 段階のため `--experimental-temporal` フラグが必要だった。Node.js 26 ではフラグなしでデフォルト有効になり、`Temporal.Now.instant()` や `Temporal.PlainDate.from(...)`、`Temporal.ZonedDateTime` などが直接利用できる。

```js
const now = Temporal.Now.zonedDateTimeISO("Asia/Tokyo");
const checkin = now.with({ hour: 15, minute: 0, second: 0 });
const stay = checkin.add({ days: 2 });
console.log(stay.toString());
```

Date のタイムゾーン・サマータイム・うるう秒周りの罠を避けつつ、不変オブジェクトとして扱えるため、サーバ側の予約・課金・スケジュール計算系コードのバグを大幅に減らせる。

### 実験的 `node:ffi` モジュール（v26.1.0）

`node:ffi` は動的ライブラリを読み込み、ネイティブシンボル（C 関数等）を JavaScript から直接呼び出せる新モジュール。Bun の `bun:ffi` や Deno の FFI に相当する機能で、ネイティブアドオン（N-API）を書かずに既存の `.so` / `.dylib` / `.dll` を呼べる。

```js
import { Library } from "node:ffi";

const lib = new Library("libm", {
  sqrt: { args: ["double"], returns: "double" },
});

console.log(lib.symbols.sqrt(2)); // 1.4142135623730951
```

利用には `--experimental-ffi` フラグが必要。Permission Model 有効時は `--allow-ffi` も必要。不正なポインタや誤ったシグネチャはプロセスクラッシュ・メモリ破壊に直結するため、信頼境界を明確にして使うこと。

### V8 14.6 / Undici 8.0

- V8 が 14.6 に更新され、`Map`/`WeakMap` の upsert メソッドなど ES 仕様の最新提案に追従。
- Undici 8.0 によって `fetch` の挙動・パフォーマンス・HTTP/2 対応周りが改善。

## 破壊的変更・移行ガイド

| 変更 | 影響 |
|------|------|
| `http.Server.prototype.writeHeader()` の削除 | `writeHead()` に書き換える |
| レガシー `_stream_readable` / `_stream_writable` / `_stream_duplex` 等のモジュール削除 | `node:stream` の公開 API に移行 |
| Readable Stream の挙動変更 | 先読みせずに 1 バッファずつ読み込むようになり、`highWaterMark` 周辺のタイミングが微妙に変わる |

特に Readable Stream の挙動変更は、ストリーミング配信系・S3 アップロード等で内部バッファリングに依存しているコードで顕在化する可能性がある。Node.js 26 を本番に上げる前に、ストリーム関連の e2e テストで挙動差分を確認しておくのが安全。

## 今後の注目点

- 2026 年 10 月に Node.js 26 が LTS 昇格予定。LTS タイミングで採用したいプロジェクトは、それまでの Current 期間中に Temporal API への移行検証を進めておくとスムーズ。
- `node:ffi` はまだ実験的だが、Bun / Deno と並んで「Node.js 上で動くスクリプトから直接ネイティブを呼ぶ」エコシステムが整いつつある。N-API アドオン作成の代替として様子見しておきたい。
- TypeScript 6.0（2026-03 リリース）と組み合わせると、Temporal の型定義もデフォルトで利用可能になり、Date 関連バグの早期発見が容易になる。
