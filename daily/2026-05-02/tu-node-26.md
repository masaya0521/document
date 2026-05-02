# Node.js 26 — Temporal API がついにデフォルト有効化

- **日付**: 2026-04-28
- **カテゴリ**: Backend / Runtime
- **ソース**: [GitHub PR #62526](https://github.com/nodejs/node/pull/62526), [Temporal 有効化 PR #61806](https://github.com/nodejs/node/pull/61806), [Issue #57127](https://github.com/nodejs/node/issues/57127), [Undici Releases](https://github.com/nodejs/undici/releases)

## 概要

Node.js v26.0.0 が Current リリースとして公開された。最大の目玉は **Temporal API のデフォルト有効化**。これまで `--experimental-temporal` フラグが必要だったが、Node.js 26 ではグローバルにそのまま `Temporal.Now.plainDateTimeISO()` などが呼べるようになった。
あわせて V8 が 14.6.202.33（Chromium 134 相当）に、HTTP クライアントの Undici が 8.0 に更新されている。Node.js 26 は本年 10 月に LTS 入りする予定で、それまでの約 6 ヶ月間は Current ラインとして提供される。

## 主な変更点

### Temporal がデフォルト有効化

- グローバル `Temporal` がフラグなしで利用可能
- `Date` オブジェクトの設計上の問題（タイムゾーン扱い、ミュータブル、ナノ秒精度の欠如など）を解消する後継 API
- 旧来の `Date` をそのまま使うコードは引き続き動作するが、新規実装では `Temporal.PlainDate` / `Temporal.ZonedDateTime` への置き換えが推奨される

```js
// 例: タイムゾーン安全な現在時刻
const now = Temporal.Now.zonedDateTimeISO('Asia/Tokyo');
console.log(now.toString()); // 2026-05-02T12:34:56.789+09:00[Asia/Tokyo]

// 期間計算もイミュータブル
const tomorrow = now.add({ days: 1 });
```

### V8 14.6 へ更新

- Chromium 134 と同等のエンジン
- ES2026 仕様の進行中提案・パフォーマンス改善・GC 改善が反映
- インライン関数最適化と V8 サンドボックスのさらなる強化

### Undici 8.0 へ更新

- `fetch` / `Headers` / `Request` / `Response` 内部実装が Undici 8 ベースに
- v7 からのマイグレーションガイドが用意されており、HTTP/2 と Pool/Agent API のシグネチャ変更に注意

### その他

- いくつかの非推奨 API の削除（詳細は CHANGELOG 参照）
- パフォーマンスフックや診断系 API の継続的な改善

## 破壊的変更・移行ガイド

- Undici 7 → 8 のマイグレーション: HTTP/2 設定オプション名の変更や `Pool` 関連 API の調整があるため、自前で `undici.Pool` を直接使っているコードは要確認
- 一部のレガシーモジュール（`punycode` 等）は廃止が進んでおり、26 系では非推奨警告がさらに増えている
- `Temporal` をすでに polyfill で導入していた場合、グローバルが衝突しうる。polyfill は外す方向で見直すのが望ましい

## 今後の注目点

- 2026-10 の LTS 入り（v26.x がアクティブ LTS に昇格）
- Temporal の標準ライブラリ統合がアプリケーションコードに与える影響（テンプレート、ORM、ロギング層での `Date` 依存をいつ剥がすか）
- V8 14.6 ベースでの WebAssembly GC / Memory64 安定化の進捗
- Node.js 25 で導入された SEA（Single Executable Applications）ビルド改善との組み合わせによるデプロイ簡易化
