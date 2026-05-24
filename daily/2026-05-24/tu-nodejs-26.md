# Node.js 26.0.0 — Temporal API 時代の幕開け

- **日付**: 2026-05-05
- **カテゴリ**: Backend / Language Runtime
- **ソース**: [GitHub Release](https://github.com/nodejs/node/releases/tag/v26.0.0), [公式ブログ](https://nodejs.org/en/blog/release/v26.0.0), [NodeSource 解説](https://nodesource.com/blog/nodejs-v26-is-here)

## 概要

Node.js 26 は 2026 年最初の Current リリースであり、JavaScript の日付・時刻処理に革命をもたらす Temporal API のデフォルト有効化が最大の目玉。V8 14.6 への更新に加え、レガシー API の大規模な削除による破壊的変更を多数含む。2026 年 10 月に LTS（Long-Term Support）へ移行予定。

## 主な変更点

### Temporal API のデフォルト有効化

従来の `Date` オブジェクトが抱えていた以下の問題を根本的に解決する新しい日時 API:

- ミュータブルなオブジェクト → **Temporal はイミュータブル**
- 暗黙のローカルタイムゾーン変換 → **明示的なタイムゾーン指定**
- 月のインデックスが 0 始まり → **直感的な 1 始まり**

```javascript
// 従来の Date
const date = new Date(2026, 4, 24); // 5月（0始まり）

// Temporal
const date = Temporal.PlainDate.from({ year: 2026, month: 5, day: 24 });
const zonedDateTime = Temporal.Now.zonedDateTimeISO('Asia/Tokyo');
```

`--harmony` フラグなしで利用可能。ビルドには Rust toolchain が必要になった点に注意。

### V8 14.6（Chromium 146 対応）

- `Map.prototype.getOrInsert()` / `getOrInsertComputed()`: キーが存在しなければ挿入する upsert 操作
- `Iterator.concat()`: 複数のイテレータを結合する `Iterator sequencing` 提案の実装

### Undici 8

組み込み HTTP クライアントが Undici 8.0.2 へアップデート。パフォーマンス改善と追加 HTTP 機能をサポート。

## 破壊的変更・移行ガイド

### 削除された API

| 対象 | 内容 | 移行先 |
|------|------|--------|
| `http.Server.prototype.writeHeader()` | 完全削除 | `writeHead()` を使用 |
| `_stream_wrap`, `_stream_readable` 等 | レガシーストリームモジュール削除 | `stream` モジュールを直接使用 |
| `--experimental-transform-types` | TypeScript 変換フラグ削除 | TypeScript の strip types が安定化済み |

### 非推奨化の昇格

- `DEP0203` / `DEP0204`（暗号化関連）: 実行時警告へ昇格
- `module.register()`: 実行時非推奨化
- ストリーム関連 `DEP0201`: 実行時非推奨化へ昇格

### ビルド要件の引き上げ

- **GCC 13.2 以上**が必須（従来は GCC 12）
- **Python 3.9 サポート廃止**
- **Rust toolchain** の新規インストールが必要（Temporal のネイティブ実装ビルド用）

## 今後の注目点

- 2026 年 10 月に **LTS（Krypton の次のコードネーム）** へ移行予定
- Temporal API の実運用での採用状況と、ライブラリエコシステムの対応
- Node.js 24（現 LTS）からの移行計画を早期に検討すべき
- Undici 8 ベースの `fetch()` のパフォーマンス検証
