# Node.js 26.1.0 — 実験的 FFI モジュールで native ライブラリ呼び出しを解禁

- **日付**: 2026-05-07（リリース）
- **カテゴリ**: Backend / Runtime
- **ソース**: [Node.js v26.1.0 Release Notes](https://nodejs.org/en/blog/release/v26.1.0), [Node.js Previous Releases](https://nodejs.org/en/about/previous-releases)

## 概要

Node.js v26.1.0 が 2026 年 5 月 7 日にリリースされた。v26 系（Current line）の最初の minor アップデートで、目玉は実験的な FFI（Foreign Function Interface）モジュールの追加。`--experimental-ffi` フラグの下で動的ライブラリのロードと、JavaScript から native symbol を呼び出すことが可能になった。これにより、これまで N-API 経由で C/C++ アドオンを書く必要があった用途について、JavaScript 側だけで native ライブラリを叩く道が拓ける。

同時に、`crypto.randomUUIDv7()` 実装の追加、`fs.stat()` への AbortSignal 対応、`statfs` の `frsize` 露出、HTTP `ClientRequest` の options merging hardening、test runner の order randomization 対応など、開発体験を地味に押し上げる改善が一通り含まれている。npm は 11.13.0 に同梱バンドルが更新されている。

## 主な変更点

### 実験的 FFI モジュール

- `node:ffi` 相当の実験 API として `--experimental-ffi` 経由で利用可能
- 動的ライブラリ（`.so` / `.dylib` / `.dll`）をロードし、関数シグネチャを宣言して呼び出す
- メモリ管理の安全性に対する責務はユーザー側にあるため、safety gate（フラグ + 警告）越しに提供
- N-API ベースのアドオン構築よりも、軽量に native API へアクセスしたいケースを想定

```js
// 例: --experimental-ffi 付きで起動
import ffi from 'node:ffi';

const libc = ffi.open('libc.so.6');
const getpid = libc.symbol('getpid', { returns: 'int', args: [] });
console.log(getpid()); // -> 現在のプロセス PID
```

（API 形状は実験中のため、最終形は変更される可能性あり）

### Crypto まわり

- `crypto.randomUUIDv7()` 新規実装。タイムスタンプベースの UUIDv7 を native で生成
- Diffie-Hellman 鍵処理のハンドリング改善

### File System

- `fs.stat()` が AbortSignal を受け付け、長時間 stat で待たされるケースをキャンセル可能に
- `statfs` の戻り値に `frsize`（fragment size）を露出

### HTTP

- `ClientRequest` の options merging を hardening。URL オブジェクトと options オブジェクトの両方を渡す際の挙動を明確化
- `IncomingMessage` で signal サポート追加

### Test Runner

- `node:test` でテスト順序のランダム化に対応（隠れた依存の検出に有用）
- mock-timer の精度・API 改善

### Utility

- `util.styleText` 等のテキストカラリングが hex カラー指定に対応

### 同梱依存の更新

- npm 11.13.0
- OpenSSL / V8 / undici 等の dependency アップデート

## 破壊的変更・移行ガイド

v26.1.0 は minor リリースのため、原則として破壊的変更はなし。FFI モジュールはフラグの下でのみ有効化されるオプトイン機能で、既存コードへの影響はない。

ただし、`ClientRequest` options merging の hardening によって、これまで暗黙に通っていた不正な options 組み合わせがエラーや警告を出すケースが起こり得る。Production 投入前に HTTP クライアントコードの動作確認を推奨。

## 今後の注目点

- FFI モジュールの stable 化に向けたフィードバックループ（メモリ安全性・型表現の API 設計）
- Deno / Bun が既に持っている FFI と機能・性能比較が始まる見込み
- N-API アドオンエコシステム（`node-gyp` / `prebuildify` 等）との棲み分け
- v26 が LTS 化される予定の 2026 年 10 月までの安定化進捗（v26 LTS の本命機能になる可能性）
