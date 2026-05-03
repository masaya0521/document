# Bun v1.3.13 — テスト isolation/parallel と install のメモリ 17x 削減

- **日付**: 2026-04-20
- **カテゴリ**: Backend（JavaScript Runtime / Toolchain）
- **ソース**: [Bun Blog — v1.3.13](https://bun.com/blog/bun-v1.3.13) / [GitHub Releases](https://github.com/oven-sh/bun/releases)

## 概要

Bun v1.3.13 は **「テストランナーの並列化」と「インストーラのメモリ効率」** を主軸にした 1.3 系のマイナーアップデート。82 issue（👍 累計 381）を解決し、JavaScriptCore へ 1,316 件の上流コミットを取り込んでいる。

特筆すべきは、**`bun test` がついに `--isolate` / `--parallel` / `--shard` / `--changed` という大規模 CI 向けの定番フラグ群を揃えた** こと、そして **`bun install` がパッケージ tarball をストリーミング展開することでメモリ消費を 17 分の 1 に削減した** こと。Bun は「速いランタイム」から「速くてスケールするツールチェーン」へと一段進化した格好。

## 主な変更点

### 1. `bun test` の並列化 4 点セット

```bash
# テストファイルごとに完全に独立したグローバル環境で実行
bun test --isolate

# 指定ワーカー数でテストファイルを分散実行
bun test --parallel
bun test --parallel=8

# CI ランナー間で決定論的に分割
bun test --shard=1/4

# git 差分に基づき影響を受けるテストファイルのみ実行
bun test --changed
```

- `--isolate`: テストファイル毎に fresh な global を作るが、トランスパイル結果はキャッシュで共有 → 速度を犠牲にしない
- `--parallel`: 自動ロードバランスで複数ワーカーに分散
- `--shard=M/N`: CI ランナー横断のテスト分割の標準パターンを公式サポート
- `--changed`: monorepo の PR ごとの実行時間を大幅短縮

Jest / Vitest 由来の CI 設計をそのまま Bun に持ち込めるようになった。

### 2. `bun install` のメモリ 17x 削減

旧来は tarball を一度全部メモリに展開してからディスクに書き出していたが、**ダウンロードしながらストリーミング展開する** 実装に変更。

- 大規模 monorepo で観測された 17x のメモリ削減
- OOM Killer に殺されがちだった CI コンテナでのインストール安定化に直結
- 「Bun を CI で使うとメモリ食う」という典型的な懸念点を解消

### 3. ソースマップのメモリ 8x 削減

VLQ デコードを毎回行う方式から、**ビット詰めバイナリ表現をオンメモリで保持する方式** に変更。スタックトレース解決が走る本番環境やテスト時のメモリプレッシャーが下がる。

### 4. zlib-ng への切り替えで gzip 5.5x 高速化

レスポンス圧縮・tarball 展開・assets 圧縮など gzip パスが広く高速化。

### 5. ランタイム側のアロケータ更新

ランタイム全体のメモリ使用量が約 5% 低下。常駐ワーカープロセスや大量の Worker を扱うサービスで効く。

### 6. 標準準拠の拡張

| 機能 | 内容 |
|---|---|
| `node:crypto` / WebCrypto | SHA3（SHA3-224 / 256 / 384 / 512）追加 |
| WebCrypto | `deriveBits()` で X25519 鍵共有 |
| WebSocket クライアント | `ws+unix://` Unix domain socket をサポート |
| `Bun.serve()` | HTTP Range request ハンドリング |

特に `Bun.serve()` の Range サポートは、メディアストリーミングや巨大ファイル配信を Bun だけで完結させるユースケースで効く。

### 7. JavaScriptCore の取り込み（1,316 commits）

- 配列 length 代入のインラインキャッシュ
- 文字列操作の最適化
- 細かなランタイム速度改善

### 8. Node.js 互換性とプラットフォーム修正

Worker のライフサイクル安定化、Windows / macOS / Linux 個別の修正多数。

## 破壊的変更・移行ガイド

メジャー破壊的変更はなし。`--isolate` を導入する場合のみ、テスト間で global state を共有していた既存テストが失敗する可能性がある（本来テスト分離されているべきなので、検出できると価値がある）。

```bash
# 段階的導入
bun test --isolate --shard=1/8  # CI で分割しつつ isolation を確認
```

## 今後の注目点

- **Vitest との立ち位置**: `--isolate / --parallel / --shard / --changed` が揃ったことで、Bun の test runner が「Vitest からの正面競合」になりつつある。Vitest 側のレスポンス
- **CI でのメモリプロファイル**: 17x 削減が大規模 monorepo の実測でどこまで効くかのコミュニティベンチマーク
- **1.4 への伏線**: 1.3 系で着実にスケールしてきたので、次の 1.4 でどのレイヤー（パッケージマネージャ / バンドラ / SQLite クライアントあたり）が大きく動くか
- **HTTP/2・HTTP/3 周辺**: `Bun.serve()` の機能拡充ペースがどう続くか
