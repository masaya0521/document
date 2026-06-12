# PostgreSQL — 19 Beta 1 リリース

- **日付**: 2026-06-12（リリースは 2026-06-04）
- **カテゴリ**: DB・Infra
- **ソース**: [公式アナウンス](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/), [PostgreSQL 19 Open Items](https://wiki.postgresql.org/wiki/PostgreSQL_19_Open_Items)

## 概要

PostgreSQL Global Development Group が PostgreSQL 19 の最初のベータ版をリリースした。18 で導入された非同期 I/O サブシステムの自動スケーリング対応、並列 autovacuum、非ブロッキングのテーブル再編成を行う `REPACK` コマンドなどパフォーマンス系の強化に加え、標準 SQL 構文によるプロパティグラフクエリ（SQL/PGQ)や `INSERT ... ON CONFLICT DO SELECT` といった開発者向け機能が多数入っている。

今後テストの進行に応じて追加のベータ・RC を経て、最終リリースは例年どおり 2026 年 9〜10 月頃の見込み。

## 主な変更点

### パフォーマンス

- **非同期 I/O の自動スケーリング**: `io_method=worker` が新設定 `io_min_workers` / `io_max_workers` に基づいて I/O ワーカー数を自動調整
- **並列 autovacuum**: `autovacuum_max_parallel_workers` で autovacuum が並列ワーカーを利用可能に。テーブルの vacuum 優先度を決める新しいスコアリングシステムも導入
- **`REPACK` コマンド**: テーブル再編成の新コマンド。`CONCURRENTLY` オプションで非ブロッキング実行が可能（`VACUUM FULL` / `CLUSTER` の代替）
- **外部キー制約**: INSERT 性能が最大 2 倍に向上
- **プランナー**: `pg_plan_advice` / `pg_stash_advice` 拡張によるプラン決定の安定化・自動適用、anti-join 最適化、インクリメンタルソートの適用範囲拡大
- **LISTEN/NOTIFY**: マルチチャネルワークロードでのスケーラビリティ改善

### 開発者向け機能

- **SQL/PGQ（プロパティグラフクエリ）**: 標準 SQL 構文でグラフクエリを実行可能に
- **`INSERT ... ON CONFLICT DO SELECT ... RETURNING`**: upsert 時に既存行を返せるように
- **`GROUP BY ALL`**: 非集約・非ウィンドウ列を自動でグループ化
- **テンポラルクエリ**: `UPDATE` / `DELETE` の `FOR PORTION OF` 句に対応
- **パーティション操作**: `ALTER TABLE ... MERGE PARTITIONS` / `SPLIT PARTITIONS`
- **jsonpath 関数拡張**: `lower()`, `upper()`, `initcap()`, `replace()`, `split_part()`, `trim()` ファミリーを追加
- **`COPY TO` のネイティブ JSON 出力**
- **`WAIT FOR LSN`**: レプリカで指定 LSN への到達を待機

### レプリケーション

- **シーケンス値のレプリケーション**: 論理レプリケーションによるオンラインアップグレードの障壁が一つ解消
- **`CREATE PUBLICATION ... EXCEPT`**: 除外テーブルの指定
- **`wal_level=replica` でも論理レプリケーションを無停止で有効化可能**（新読み取り専用パラメータ `effective_wal_level`）

### 監視・セキュリティ

- 新統計ビュー `pg_stat_lock`（ロック統計）、`pg_stat_recovery`（リカバリ状態）
- `EXPLAIN ANALYZE` に `IO` オプション（非同期 I/O 統計の表示）
- `log_min_messages` をプロセスタイプ別に指定可能
- **SNI 対応**: `pg_hosts.conf` で複数 TLS 証明書を管理可能
- データチェックサムのオンライン有効化 / 無効化

## 破壊的変更・移行ガイド

- **JIT コンパイルがデフォルト無効化**: JIT に依存した分析系ワークロードはアップグレード後に `jit=on` の明示設定が必要
- **`default_toast_compression` のデフォルトが `lz4` に変更**: pglz 前提のストレージ見積もりは再確認が必要
- **RADIUS 認証のサポート廃止**: 利用中の場合は他の認証方式への移行が必須
- **`vacuumdb --analyze-only`**: デフォルトでパーティション化テーブルも分析対象に変更
- クライアント側で **MD5 認証の警告** が表示されるようになった（`md5_password_warnings` で制御可）

ベータ期間中に仕様が変わる可能性があるため、本番適用は不可だが、典型的なワークロードでの互換性テストが推奨されている。

## 今後の注目点

- 追加ベータ → RC → 2026 年 9〜10 月頃の GA というスケジュール
- JIT デフォルト無効化が GA までに維持されるか（ベータでのフィードバック次第で変わる可能性）
- SQL/PGQ の対応範囲拡大（グラフ DB ワークロードの取り込み）
- `REPACK CONCURRENTLY` の実運用での安定性（`pg_repack` 拡張からの移行可否）
