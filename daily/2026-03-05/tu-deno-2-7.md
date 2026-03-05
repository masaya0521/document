# Deno 2.7 — Temporal API 安定化とスタンドアロンコンパイル

- **日付**: 2026-03-05
- **カテゴリ**: Backend
- **ソース**: [公式ブログ](https://deno.com/blog/v2.7), [GitHub Release](https://github.com/denoland/deno/releases/tag/v2.7.0)

## 概要

Deno 2.7 は 2026 年 2 月 25 日にリリースされた。最大の目玉は Temporal API の安定化で、`--unstable-temporal` フラグが不要になった。Chrome 144 が 2026 年 1 月に Temporal を出荷したことを受け、V8 14.5 へのアップグレードとともに安定版に昇格した。また、Windows ARM のネイティブビルド対応や、npm パッケージのスタンドアロン実行ファイルへのコンパイル機能も追加されている。

## 主な変更点

### Temporal API の安定化

JavaScript の日付・時刻処理における長年の課題を解決する Temporal API が安定化。`Date` オブジェクトの問題点（ミュータブル、タイムゾーン処理の不備、月のゼロインデックス等）を根本的に解消する。

```typescript
// 現在の日付を取得（イミュータブル）
const today = Temporal.Now.plainDateISO();

// 1 ヶ月後の日付（元のオブジェクトは変更されない）
const nextMonth = today.add({ months: 1 });

// タイムゾーン間の変換
const tokyoMeeting = Temporal.ZonedDateTime.from({
  timeZone: "Asia/Tokyo",
  year: 2026,
  month: 3,
  day: 5,
  hour: 15,
  minute: 0,
});
const nyTime = tokyoMeeting.withTimeZone("America/New_York");
```

### Windows ARM ネイティブビルド

`aarch64-pc-windows-msvc` ターゲットの公式ビルドが提供開始。Surface Pro X や ThinkPad X13s 等の ARM ベース Windows デバイスで、x86 エミュレーションなしにネイティブパフォーマンスで動作する。

### `deno create` コマンド

プロジェクトのスキャフォールディング用コマンド。npm と JSR の両パッケージに対応。

```bash
deno create vite my-app
deno create @std/fresh my-fresh-app
```

### npm パッケージのスタンドアロンコンパイル

グローバルインストール時に npm パッケージをスタンドアロン実行ファイルにコンパイル可能に。

### 新しいサブプロセス API

`Deno.Command` API の便利な代替として、3 つの新しい関数が追加：

- `Deno.spawn()` — 非同期でサブプロセスを起動
- `Deno.spawnAndWait()` — 非同期で起動し、完了を待機
- `Deno.spawnAndWaitSync()` — 同期版

### V8 14.5 へのアップグレード

最新の V8 エンジンにより、パフォーマンス改善、バグ修正、新しい JavaScript 機能が利用可能に。

### Node.js 互換性の改善

- `node:worker_threads` の互換性向上
- `node:child_process` の改善
- `node:zlib` の互換性向上
- `--check-js` フラグによる JavaScript のみプロジェクトの型チェック対応

## 今後の注目点

- Temporal API は Chrome 144 でも利用可能になり、ブラウザとサーバーサイドの両方で統一的な日時処理が可能に
- Deno の Node.js 互換性は各リリースで着実に向上しており、既存 Node.js プロジェクトからの移行障壁が低下
- 2.7.2 パッチ（2026-03-03）で早速バグ修正がリリースされている
