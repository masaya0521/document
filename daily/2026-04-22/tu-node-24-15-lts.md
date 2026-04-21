# Node.js 24.15.0 LTS (Krypton) — 主要な変更と移行ポイント

- **日付**: 2026-04-22
- **カテゴリ**: Backend / Runtime
- **ソース**: [Node.js Previous Releases](https://nodejs.org/en/about/previous-releases), [Vercel Changelog](https://vercel.com/changelog/node-js-24-lts-is-now-generally-available-for-builds-and-functions), [Node.js 24 (Krypton) promoted to LTS](https://progosling.com/en/dev-digest/2025-11/nodejs-24-lts-krypton)

## 概要

Node.js 24 系列は 2025 年 10 月に Active LTS に昇格したコードネーム **Krypton** のメジャーライン。その 6 ヶ月目のパッチとして 2026-04-15 に **24.15.0** が配信された。LTS の公式サポートは 2028-04-30 まで確保されている。

24 系は V8 13.6 を搭載し、`Float16Array` と `Error.isError`、グローバル `URLPattern`、`Undici v7`、npm 11 を標準装備する「Web 標準志向の強い LTS」として位置付けられる。24.15.0 はこれらの API 群を保守フェーズで安定させつつ、セキュリティと HTTP 周りの修正を積む位置付けのリリース。

## 主な変更点

### V8 13.6 と新しい JS 機能

- **`Float16Array`**: 16bit 浮動小数点の TypedArray。機械学習の推論（重みが FP16 前提）、WebGPU との相互運用、メモリ制約のある数値処理で効く。
- **`Error.isError(value)`**: クロス realm（vm コンテキスト / Worker 間）でも `Error` を正確に判別できる新しい標準 API。従来の `instanceof Error` や `Object.prototype.toString` より堅牢。

```js
const buf = new Float16Array([1.5, 2.25, 3.125]);
console.log(Error.isError(new TypeError()));  // true
```

### グローバル `URLPattern`

外部ライブラリや正規表現に頼らず、Web 標準のパターンマッチで URL ルーティングができる。

```js
const pattern = new URLPattern({ pathname: '/users/:id' });
const match = pattern.exec('https://example.com/users/42');
console.log(match?.pathname.groups.id); // "42"
```

Service Worker や Cloudflare Workers、Deno、Bun と同じ API で書けるため、ルーティングロジックの共有がしやすくなる。

### Undici v7（組み込み `fetch`）

`fetch` の実装が Undici v7 に刷新され、次のような強化が入った。

- より厳密な Fetch 仕様準拠
- インターセプター API（プロキシやリトライなどミドルウェア的な差し込みがしやすい）
- `WebSocketStream` による WebSocket ハンドリング
- HTTP/2・HTTP/3 周りの改善、コネクション再利用の効率化

### その他

- `AsyncLocalStorage` が既定で `AsyncContextFrame` 実装を使用し、async hooks のオーバーヘッドが下がる。
- 実験的権限フラグが `--experimental-permission` → `--permission` に簡素化。
- npm 11 を同梱。

## 破壊的変更・移行ガイド

- **対応終了プラットフォーム**: 32-bit Linux on armv7 は 24 以降でサポートされない。Raspberry Pi 2 世代の ARM で動かしているワーカーは 64-bit 化が必要。
- **HTTP 挙動の変化**: Undici v7 への置き換えで、ゆるく動いていた不正な fetch 呼び出しが失敗するケースがある。特にリクエストボディの型、`Referrer-Policy` 周り、CORS 相当のバリデーションに注意。
- **`--experimental-permission`**: フラグ名を `--permission` へ置換。CI スクリプトや Dockerfile での指定を更新する。
- **TypeScript 型の互換性**: グローバル追加（`URLPattern` 等）により、自前で定義していた型が重複する可能性がある。`@types/node` を同バージョン帯に揃える。

### 推奨移行手順

1. CI で Node 24 のマトリクスを追加し、現行 LTS（Node 22）と並走させる。
2. `npm 11` 系で `package-lock.json` が再生成されるため、依存解決の差分をレビュー。
3. 自前 fetch ラッパーがある場合、Undici v7 のインターセプターに置き換えを検討。
4. シングルバイナリ配布（SEA）や `--permission` を使うチームは、フラグ命名と制約範囲を再確認。

## 今後の注目点

- **Node 26 系**: TypeScript の透過実行（`--experimental-strip-types`）が既定化される見込みで、型消去だけで動くコードはほぼノー設定で実行できるようになる流れ。
- **Permission Model**: `--permission` がフラグとして安定したことで、サーバーサイド JS の権限境界（ファイル / ネット / 子プロセス）がコンテナ外の守りとして意識されるようになっている。
- **LTS サポート窓**: 24 のサポートは 2028-04-30 まで。22 LTS（Jod）は 2027-04-30 に終了するので、本番クラスタは 2026〜2027 内に 24 へ切り替える計画を立てるタイミング。
