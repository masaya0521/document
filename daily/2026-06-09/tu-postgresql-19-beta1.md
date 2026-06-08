# PostgreSQL 19 Beta 1 — 並列オートバキュームと SQL/PGQ、破壊的変更

- **日付**: 2026-06-09
- **カテゴリ**: DB・Infra
- **ソース**: [PostgreSQL 19 Beta 1 Released!](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/), [Release 19 Notes](https://www.postgresql.org/docs/19/release-19.html)

## 概要

PostgreSQL Global Development Group は 2026年6月4日、PostgreSQL 19 の Beta 1 をリリースした。PostgreSQL 18 で導入された非同期 I/O（AIO）基盤をさらに発展させ、並列オートバキュームや FK 制約時のインサート性能改善といったパフォーマンス強化に加え、SQL/PGQ によるプロパティグラフクエリ、温度的（temporal）データ操作の拡張など、SQL 機能面でも大きな前進が見られる。

正式リリース（GA）は 2026年9月〜10月を予定しており、Beta 期間は本番採用前の互換性検証・性能検証の機会となる。一方で JIT のデフォルト無効化や TOAST 圧縮のデフォルト変更など、移行時に注意すべき破壊的変更も含まれている。

## 主な変更点

### パフォーマンス

- **並列オートバキューム**: オートバキュームが複数ワーカーで並列実行され、大規模テーブルのバキューム時間を短縮。
- **非同期 I/O の自動スケーリング**: `io_method=worker` が新設の `io_min_workers` / `io_max_workers` に基づき I/O ワーカー数を自動調整。`EXPLAIN ANALYZE` の `IO` オプションで AIO 統計を可視化できるようになった。
- **インサート性能の向上**: 外部キー制約のあるテーブルへのインサートが最大2倍高速化。
- **プランナー最適化**: アンチジョインや段階的（incremental）ソートの最適化。

### SQL 機能

- **SQL/PGQ（Property Graph Queries）**: 標準 SQL の枠組みでプロパティグラフクエリを実行可能に。
- **`UPDATE / DELETE ... FOR PORTION OF`**: 時間レンジ（temporal range）に対する部分更新・削除をサポート。
- **`ALTER TABLE ... MERGE / SPLIT PARTITIONS`**: パーティションの結合・分割によるオンライン再編成。
- **`GROUP BY ALL`**: 集約関数以外の全列で自動グルーピングする糖衣構文。
- **`INSERT ... ON CONFLICT DO SELECT ... RETURNING`**: コンフリクト時に既存行を SELECT して返却。

### レプリケーション

- 論理レプリケーションで **シーケンス値をレプリケート** 可能に。
- `CREATE PUBLICATION ... EXCEPT` で除外テーブルを指定可能。
- サーバー再起動なしで論理レプリケーションを有効化可能。
- `postgres_fdw` で配列演算をプッシュダウン。

### 開発者・運用機能

- **`WAIT FOR LSN`**: レプリカで指定 LSN の到達を待ち、読み取り一貫性を確保。
- **`pg_stat_lock` / `pg_stat_recovery` ビュー**: ロック統計・リカバリ状態の可視化。
- 統計ビューへの `stats_reset` 列追加、プロセスタイプごとのログレベル指定。
- PL/Python がイベントトリガーをサポート。

## 破壊的変更・移行ガイド

- **JIT がデフォルト無効化**: これまで `jit = on` がデフォルトだったが無効に変更。JIT に依存していたワークロードは明示的に有効化が必要。逆に JIT 起因のプラン遅延に悩んでいた環境では恩恵となる。
- **`default_toast_compression` が `lz4` に変更**: 従来の `pglz` から変更。新規 TOAST データの圧縮形式が変わるため、ディスク使用量・CPU 特性を再評価する。
- **RADIUS 認証サポート廃止**: RADIUS を使った認証構成は移行が必要。

## 今後の注目点

- GA（9〜10月予定）までに Beta 2 / RC が出る見込み。本番採用前に並列オートバキュームの I/O 負荷、AIO ワーカー自動スケールの挙動を検証したい。
- SQL/PGQ はグラフ DB の代替として注目される機能。実運用でのクエリプランナ最適化の成熟度を見極めたい。
- JIT デフォルト無効化により、JIT 前提でチューニングしていた OLAP ワークロードはプラン退行が起きないか確認が必要。
