# Node.js 26 — Temporal API デフォルト有効化と主要な破壊的変更

- **日付**: 2026-05-05（リリース日）
- **カテゴリ**: Backend / Language Runtime
- **ソース**: [GitHub Release](https://github.com/nodejs/node/releases/tag/v26.0.0), [公式ブログ](https://nodejs.org/en/blog/release/v26.0.0)

## 概要

Node.js 26 は 2026年5月5日にリリースされた Current リリースで、10月に LTS へ移行予定。最大の目玉は **Temporal API のデフォルト有効化** で、長年 `--experimental-temporal` フラグが必要だった最新の日時 API がフラグなしで利用可能になった。V8 エンジンは 14.6 へ更新され、`Map.prototype.getOrInsert()` や `Iterator.concat()` などの新しい JavaScript 言語機能が利用可能。

## 主な変更点

### Temporal API（デフォルト有効化）

JavaScript の `Date` オブジェクトの後継として設計された Temporal API が、フラグなしで利用可能になった。タイムゾーンの正確な扱い、不変性、期間計算などレガシーな `Date` が苦手としていた領域をカバーする。

```javascript
// タイムゾーンを考慮した日時操作
const now = Temporal.Now.zonedDateTimeISO('Asia/Tokyo');
const oneWeekLater = now.add({ weeks: 1 });

// 期間計算
const duration = now.until(oneWeekLater);
console.log(duration.toString()); // "P7D"

// PlainDate（時刻情報なし）
const date = Temporal.PlainDate.from('2026-05-26');
const nextMonth = date.add({ months: 1 });
```

### V8 14.6 エンジン更新

Chromium 146 相当の V8 エンジンに更新され、以下の言語機能が追加。

- **`Map.prototype.getOrInsert()` / `getOrInsertComputed()`**: Map にキーが存在しない場合のデフォルト値挿入を1操作で実行
- **`Iterator.concat()`**: 複数のイテレータを連結

```javascript
// Map upsert パターン
const map = new Map();
const value = map.getOrInsert('key', 'default'); // 'default'

// Iterator concat
const combined = Iterator.concat([1, 2], [3, 4]);
console.log([...combined]); // [1, 2, 3, 4]
```

### Undici 8

組み込み HTTP クライアント（`fetch()` の内部実装）が Undici 8.0.2 へ更新。パフォーマンス改善と HTTP 機能の追加。

## 破壊的変更・移行ガイド

### 削除された API

| 項目 | 対応 |
|------|------|
| `http.Server.prototype.writeHeader()` | `writeHead()` に置換 |
| `_stream_wrap`, `_stream_readable` 等のレガシーストリームモジュール | `stream` モジュールのサブクラスを使用 |
| `--experimental-transform-types` フラグ | 不要になったため削除 |

### ランタイム非推奨化

- `module.register()` — ローダーフックの登録方法が変更
- 暗号関連の DEP0203, DEP0204

### ビルド要件の引き上げ

- **GCC**: 13.2 以上が必要
- **Python**: 3.9 サポート廃止（3.10 以上が必要）
- **NODE_MODULE_VERSION**: 147 に更新（ネイティブアドオンの再ビルドが必要）

### 移行チェックリスト

1. `writeHeader()` を使用している箇所を `writeHead()` に変更
2. レガシーストリームモジュール（`_stream_*`）のインポートを `stream` に変更
3. ネイティブアドオン（N-API 以外）を Node.js 26 向けに再ビルド
4. CI のビルド環境の GCC / Python バージョンを確認

## 今後の注目点

- **2026年10月**: Node.js 26 が LTS（Long-Term Support）に移行
- **Temporal API の普及**: フラグなしで使えるようになったことで、ライブラリやフレームワークでの採用が加速する見込み
- **Node.js 24 LTS**: 引き続き 2028年4月まで長期サポート。急ぎの移行は不要
- **Node.js 27**: 2026年10月に Current リリース予定
