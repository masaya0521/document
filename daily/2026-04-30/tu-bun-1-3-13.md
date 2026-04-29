# Bun v1.3.13 — テストランナーの parallel/isolate/shard 化と install のメモリ 17 倍削減

- **日付**: 2026-04-19
- **カテゴリ**: Backend Runtime / Test Tool
- **ソース**: [Bun Blog: Bun v1.3.13](https://bun.com/blog/bun-v1.3.13), [Bun Releases](https://github.com/oven-sh/bun/releases)

## 概要

Bun v1.3.13 は、テストランナーと install まわりに大きく踏み込んだリリース。今までも `bun test` の高速さは Vitest / Jest との比較で武器にされてきたが、今回 `--parallel`, `--isolate`, `--shard`, `--changed` の 4 フラグが揃ったことで、CI を含めた本格的なテスト分散実行が単体ツールで完結するようになった。並行して `bun install` 側はメモリ消費を従来の 1/17 まで削減。SHA3 や Range request 対応など、Node.js 互換性向上と Web 標準のカバレッジ拡大も継続している。

直前の v1.3.12（4/20）で Bun.WebView や Markdown レンダリングといった派手な機能が追加されていたのに対し、v1.3.13（4/19）は地味だが「日常的に効く」改善が並ぶアップデート。82 件の issue 修正と JavaScriptCore エンジンの 1316 コミット分のアップグレードを含む。

> 注: blog の公開日付の前後関係上、v1.3.13 → v1.3.12 の順に並ぶことがあるが、このノートは v1.3.13 のリリースノートを基準に整理している。

## 主な変更点

### `bun test` の分散実行フラグ群

- **`--isolate`**: 各テストファイルを「同一プロセス内の新しいグローバル環境」で実行する。ファイル間でマイクロタスクを drain し、ソケットを close、タイマーをキャンセルする。**プロセス起動コストを払わずに**ファイル間のグローバル汚染を防げるのが特徴で、jest の `--isolateModules` よりも軽量。
- **`--parallel`**: ワーカープロセスにテストファイルを配分（既定値は CPU コア数）。キャッシュ局所性を意識してファイルを分割し、idle になったワーカーが他のキューから work-stealing する設計。
- **`--shard=M/N`**: CI 上で M 番目（全 N 個）のシャードのみ実行。Jest / Vitest / Playwright と同じ構文なので、既存 CI 設定をそのまま流用しやすい。
- **`--changed`**: ブランチ上の git 差分を検出し、import グラフから影響を受けるテストファイルのみ実行。CI でも feature ブランチの fast feedback ループを作りやすくなった。

```bash
# 例: GitHub Actions の matrix で 4 シャードに分散
bun test --shard=${{ matrix.shard }}/4 --parallel

# ローカルで変更影響範囲だけ素早く回す
bun test --changed --isolate
```

### `bun install` のメモリ削減（17 倍）

- tarball を「ダウンロードしながらストリーム展開」する実装に変更。圧縮バイト分のみメモリに保持し、展開済みファイルを丸ごと bufferd に持たない。
- 結果として、大規模 monorepo の cold install や CI のコンテナ環境でのメモリピークが大幅に低下。OOM で死にがちな小さい CI ランナーでも完走しやすくなる。

### 暗号機能の拡充

- WebCrypto / `node:crypto` の双方で **SHA3-224 / 256 / 384 / 512** に対応。`crypto.createHash('sha3-256')` や `crypto.subtle.digest('SHA3-256', data)` がそのまま動く。
- SubtleCrypto の `deriveBits()` が **X25519** に完全対応。ECDH 系のキー導出を WebCrypto API のみで完結できるように。

### `Bun.serve()` の HTTP セマンティクス強化

- **Range request 対応**: クライアントから `Range: bytes=...` が来た場合、`206 Partial Content` で応答（RFC 9110 準拠）。動画／大容量ファイル配信の seek やレジューム DL をサーバ側コードを変えずに扱える。
- **大容量ファイルストリーミング**: SSL 上 / Windows でも段階的にストリーミング。peak memory が下がる。

### WebSocket: Unix domain socket 接続

- `ws+unix://` / `wss+unix://` URL スキームをサポート。同一ホスト上のプロセス間通信を WebSocket クライアント API で書けるようになった。サイドカープロセス・ヘルパープロセスとのリアルタイム通信が薄いコードで書ける。

### その他のパフォーマンス改善

- **gzip 5.5 倍高速化**: 圧縮ライブラリを zlib-ng にアップグレード。`Bun.serve()` の Content-Encoding: gzip 応答や、HTTP クライアント側の gzip 解凍が高速化。
- **ソースマップ メモリ 8 倍削減**: 1 マッピングあたり 2.4 バイトの新フォーマットでメモリにロードする。スタックトレース解決時の RSS 増加を抑える。
- **JavaScriptCore 1316 コミットアップグレード**: V8 / SpiderMonkey に追従する形で、最新 JS 仕様の挙動・最適化が更新。

## 破壊的変更・移行ガイド

破壊的変更は基本的にない。`--isolate` / `--parallel` はオプトインのフラグなので、既存の `bun test` スクリプトはそのまま動く。`bun install` のストリーミング展開も外部から見て挙動互換。

注意点としては:

- `--parallel` でテストを並列化すると、これまで暗黙のうちに「同一ファイル順序」を前提にしていたテストが失敗するケースがある（テスト実装側の問題）。`bun test --parallel` で fail するなら、グローバル状態に依存しているテストを洗い出すきっかけにできる。
- WebSocket の `ws+unix://` は新規スキームなので、既存ライブラリ側で URL バリデーションが厳しいものは事前確認が必要。

## 今後の注目点

- `bun test` が parallel / isolate / shard / changed を揃えたことで、Vitest を独自スタックの選択肢として置き換えられるかが今後の焦点。Vitest 4.x 系も browser モードで Playwright 連携を進めており、Bun と Vitest の差分が「Web ブラウザでテストするか / Bun ランタイムでテストするか」に収束しつつある。
- `bun install` のメモリ削減は、巨大 monorepo の CI 体験を地味に底上げする。pnpm v11 の SQLite ストアと合わせて「2026 年は install まわりが軽くなる年」と言える。
- SHA3 / X25519 / Range request 対応は Web 標準・Node.js 標準の両方に追従するロードマップ通りの一手で、今後も「標準 API のカバレッジ完成度」が Bun の差別化軸になっていきそう。
