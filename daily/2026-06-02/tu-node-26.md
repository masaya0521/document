# Node.js 26 — Temporal API デフォルト有効化

- **日付**: 2026-06-02（v26.0.0 は 2026-05-05、v26.2.0 は 2026-05-20 リリース）
- **カテゴリ**: Backend / Language（ランタイム）
- **ソース**: [Release v26.0.0](https://github.com/nodejs/node/releases/tag/v26.0.0), [公式リリースブログ](https://nodejs.org/en/blog/release/v26.0.0), [v26.2.0](https://github.com/nodejs/node/releases/tag/v26.2.0)

## 概要

Node.js 26.0.0 が 2026年5月5日に Current 版としてリリースされた。最大の目玉は **Temporal API がフラグなしでデフォルト有効化**されたこと。標準の `Date` オブジェクトが抱えていた可変性・タイムゾーンの曖昧さ・直感的でない日付演算といった長年の課題に対する現代的な代替が、ついに標準ランタイムで利用可能になった。V8 は 14.6（Chromium 146 相当）へ更新され、HTTP クライアントの Undici も 8 系へ上がっている。Node 26 は Current として約6ヶ月運用された後、2026年10月に Active LTS へ移行する予定。

## 主な変更点

### Temporal API がデフォルト有効化

`Temporal` はイミュータブルな日時オブジェクト、明示的なタイムゾーン処理、予測可能な日付演算を提供する。Chrome 144（2026年1月）に続き、Deno 2.7 も安定化しており、ランタイム横断で利用可能なフェーズに入った。

```javascript
// イミュータブルで明示的なタイムゾーン指定
const zoned = Temporal.ZonedDateTime.from("2026-06-02T09:00[Asia/Tokyo]");
const tomorrow = zoned.add({ days: 1 }); // 元のオブジェクトは不変
```

### V8 14.6 の新機能

- **Upsert 操作**: `Map.prototype.getOrInsert()` / `getOrInsertComputed()`（`WeakMap` 版も）でマップへの条件付き挿入が簡潔に書けるようになった。
- **Iterator sequencing**: `Iterator.concat()` で複数イテレータを連結可能。

```javascript
const cache = new Map();
// キーが無ければ計算して挿入、あれば既存値を返す
const value = cache.getOrInsertComputed(key, () => expensiveCompute(key));
```

### Undici 8 同梱

`fetch` を支える HTTP クライアントが Undici 8.0.2 へ更新され、新機能と性能改善が取り込まれた。

### その他

- v26.2.0（5/20）など、Current 版として継続的にマイナーアップデートが進行中。

## 破壊的変更・移行ガイド

メジャーリリースのため後方互換性のない削除がある。アップグレード時は以下を確認すること。

- **レガシーストリームモジュール削除**: `_stream_wrap` / `_stream_readable` / `_stream_writable` / `_stream_duplex` / `_stream_transform` / `_stream_passthrough` が完全削除。内部 API に依存する古いパッケージは要注意。
- **`http.Server.prototype.writeHeader()` 削除**: `writeHead()` へ置き換える。
- **`module.register()` が実行時非推奨化**。
- **ビルド要件の引き上げ**: GCC 13.2 が必要に。Python 3.9 サポートを廃止。
- **MSVC 非対応**（Node 24 以降）も引き続き。

移行時はまず CI を Node 26 で回し、`--pending-deprecation` フラグで非推奨 API の使用箇所を洗い出すとよい。LTS を待つ運用なら、本番投入は 2026年10月の Active LTS 化以降が無難。

## 今後の注目点

- 2026年10月の Active LTS 化。それまでは Current として破壊的変更を含むマイナーが入りうる。
- Temporal のエコシステム対応（date-fns / Luxon 等のライブラリが Temporal ベースへ移行するか）。
- Undici 8 系の `fetch` 挙動変更が既存コードに影響しないかの検証。
