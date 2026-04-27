# Bun v1.3.13 — テストランナー強化とメモリ効率の大幅改善

- **日付**: 2026-04-27
- **カテゴリ**: Backend / Runtime
- **ソース**: [Bun v1.3.13 リリースブログ](https://bun.com/blog/bun-v1.3.13), [GitHub Releases](https://github.com/oven-sh/bun/releases)

## 概要

Bun は 2026-04-19 に **v1.3.13** を公開した。今回の目玉は **`bun test` の本格的な並列・分散・差分実行サポート**と、`bun install` のストリーミング展開によるメモリ削減（17×）。さらに `zlib-ng` 採用による gzip 高速化、`Bun.serve()` の Range request 対応、`node:crypto` / WebCrypto への SHA3 / X25519 追加など、Node.js 互換と本番運用の双方を底上げする変更が並ぶ。82 件の issue を解消し、関連リアクションは合計 381。

## 主な変更点

### `bun test` の並列・分離・分散・差分実行

- **`--parallel[=N]`**: テストファイルを最大 N 個のワーカープロセスへ分散。「ファイルはキャッシュ局所性のためにパーティション化され、空いたワーカーが最も忙しいキューから work-steal する」と説明されている。
- **`--isolate`**: 各テストファイルを**独立したグローバル**で実行。ファイル間でマイクロタスクをドレイン、ソケットを閉じ、タイマーをキャンセルする。
- **`--shard=M/N`**: パス順ソート＋ラウンドロビンで CI ジョブ分割を実現。
- **`--changed`**: git の変更影響を受けたテストだけを実行。`--changed=HEAD~1` のように比較先も指定可能。

```bash
# 4 プロセス並列、独立グローバル、PR 差分のみ
bun test --parallel=4 --isolate --changed=origin/main

# CI を 5 シャードに分割
bun test --shard=2/5
```

### `bun install` のストリーミング展開

> "bun install now extracts package tarballs **while they are still downloading**"

これによりインストール時のメモリ使用量が **17 倍削減**。ピア依存が多いモノレポでの分離リンカ最適化と組み合わせると、**20.5 秒 → 2.4 秒** のインストール短縮例も示されている。

### ソースマップのビット圧縮

ビット圧縮形式の導入で、ソースマップ表現が **11.3MB → 1.29MB（約 2.4 バイト/マッピング）** に。プロセス全体のメモリ削減量は 3.3% 程度ではあるが、巨大バンドルを抱える環境では効いてくる。

### gzip / deflate の高速化（zlib-ng 採用）

- `gzipSync html-128K L1`: 275µs → 107µs（**2.59×**）
- `deflate 123K L6`: 373µs → 68µs（**5.48×**）

`Bun.gzipSync` / `Bun.deflateSync` を使う API ゲートウェイや SSR レスポンス圧縮で素直に効く。

### 暗号機能の拡張

- `crypto.createHash("sha3-256")` などで **SHA3-224/256/384/512** をサポート。WebCrypto からも利用可能。
- `crypto.subtle.deriveBits()` で **X25519 鍵合意**を完全実装。

### ネットワーク機能

- **`Bun.serve()` が Range リクエスト対応**。動画配信や大容量ダウンロードで `206 Partial Content` を返せる。
- WebSocket クライアントが **`ws+unix:///tmp/app.sock`** スキームで Unix domain socket に接続可能。TLS 版 `wss+unix://` も提供。

### バグ修正のハイライト

Worker 関連クラッシュ、TLS 設定、`process.ppid` のキャッシング、WebSocket プロキシ、CSS `@layer` 処理など、Node.js 互換と安定性に関わる根本修正を含む。

## 今後の注目点

- **`bun test` のシャード／差分実行は CI 時間に直接効く**ため、Jest や Vitest からの移行検討材料が一段増えた印象。`--changed` は monorepo の影響範囲テストに刺さる。
- ストリーミング tarball 展開は、コンテナビルドや CI のキャッシュ戦略（メモリ Tight な環境）と相性が良い。
- SHA3 / X25519 の追加で、Node.js 互換のセキュリティ実装の選択肢が広がる。WebCrypto 経由でブラウザと同等 API が使える点が地味に大きい。
- Range リクエストや `ws+unix://` の対応は、Bun.serve をフロントの SSR/エッジサーバとして使うユースケースを後押しする変化。
