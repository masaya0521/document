# Bun 1.3.13 — `bun test` がついに parallel / isolate を獲得

- **日付**: 2026-05-13
- **カテゴリ**: Backend / Dev Tool
- **ソース**: [Bun Blog (v1.3.13)](https://bun.com/blog/bun-v1.3.13), [Bun on X](https://x.com/bunjavascript/status/2046148376186789963)

## 概要

Bun v1.3.13 は 82 issue を修正したマイナーリリースだが、テストランナーまわりに **`--parallel` / `--isolate` / `--shard` / `--changed`** という Jest / Vitest / Playwright と互換性のあるフラグが一気に加わった。これにより、Bun を「速いランタイム」ではなく「Jest 系の置き換えとして CI でも使えるテストランナー」として真面目に検討できる水準になった。

加えて `bun install` のメモリ使用量が最大 1/17、source map のメモリ使用量が 1/8 になっており、CI で大規模モノレポを扱うときに刺さる改善が並ぶ。`gzip` も zlib-ng で 5.5x 高速化されている。

## 主な変更点

### `bun test --parallel`

- 全 CPU コアを使ってファイル単位で並列実行
- `--parallel=8` のようにワーカー数も指定可能
- `JEST_WORKER_ID` / `BUN_TEST_WORKER_ID` 環境変数がセットされるので、ワーカーごとに DB やポートを分けたいときに使える
- Jest / Vitest からの移行時にスクリプトを書き換えずに済む

### `bun test --isolate`

- ファイルごとに global を作り直す
- グローバルを汚すテストが他ファイルに漏れない
- 並列実行と組み合わせるのが本命の使い方

### `bun test --shard`

- `--shard=1/4` のような構文で CI ランナー間に分割
- Jest / Vitest / Playwright と同じ書き方
- 内部的にはファイルパスでソートしたうえで round-robin に割り振り、シャード間のバランスを ±1 ファイル以内に保つ
- GitHub Actions の matrix と組み合わせて並列 CI を組みやすい

### `bun test --changed`

- 直近の変更ファイルに関連するテストだけ実行する
- ローカル開発で「触ったところだけ素早く回す」ユースケース向け

これらは既存の `--bail` / `--randomize` / `--dots` / JUnit reporter / LCOV coverage / snapshot と組み合わせて使える。

### パフォーマンス系

- `bun install`: タールボールをディスクへストリーミングし、ピークメモリを最大 1/17 に
- ソースマップのメモリ使用量を 1/8 に
- ランタイムメモリを 5% 削減
- gzip 解凍を zlib-ng ベースに切り替えて 5.5x 高速化

### Node.js 互換

- `node:crypto` / WebCrypto で SHA3 をサポート
- `Bun.serve()` で Range request 対応
- `ws+unix://` プロトコルの WebSocket クライアント

## 破壊的変更・移行ガイド

破壊的変更は基本ない。フラグはすべてオプトインで、既存の `bun test` の挙動は据え置き。

Jest / Vitest から移行する場合の置き換え対応：

| 移行元 | Bun |
|--------|-----|
| `jest --maxWorkers=4` | `bun test --parallel=4` |
| `jest --shard=1/3` | `bun test --shard=1/3` |
| `vitest --isolate` | `bun test --isolate` |
| `jest --onlyChanged` | `bun test --changed` |

`--isolate` は Vitest と同じく「ファイルごとに global を分離」する意味で、Jest の「ワーカープロセス分離」とは厳密にはレイヤーが違う点だけ注意。

## 今後の注目点

- これで Bun のテストランナーは Jest / Vitest と機能パリティに近づいたため、CI での Bun 採用がさらに進む可能性がある
- 並列実行に依存する flaky test の洗い出しが必要になる（既存テストが暗黙にシリアル実行を前提にしているケースがある）
- `bun install` のメモリ削減は大規模モノレポでの CI コスト削減に効くため、Yarn Berry / pnpm との比較が再燃する見込み
- 2026/4 の `Bun.WebView`（v1.3.12）と合わせて、ブラウザ E2E ランナーとしての立ち位置を狙う流れが続きそう
