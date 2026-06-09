# PostgreSQL 19 Beta 1 — プロパティグラフ・並列 autovacuum・REPACK

- **日付**: 2026-06-10（リリース: 2026-06-04）
- **カテゴリ**: DB・Infra
- **ソース**: [PostgreSQL: PostgreSQL 19 Beta 1 Released!](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/), [Release 19 Notes](https://www.postgresql.org/docs/19/release-19.html)

## 概要

PostgreSQL 19 Beta 1 が 2026年6月4日にリリースされた。SQL 標準のプロパティグラフ問い合わせ（SQL/PGQ）、upsert の表現力強化、運用面では並列 autovacuum や非ブロッキングな `REPACK` といった、開発者・DBA の双方に効く機能が揃う。GA（正式版）は例年どおり 2026年9〜10月頃が見込まれており、本番投入前に検証しておきたい変更が多い。

注意点として、**JIT がデフォルト無効化**、**`default_toast_compression` のデフォルトが `lz4` に変更**、**RADIUS 認証の削除**・**md5 認証の deprecate** など、デフォルト挙動の変更が含まれる。

## 主な変更点

### 開発者向け（SQL 機能）

- **SQL/PGQ プロパティグラフ**: SQL 標準構文でグラフクエリをネイティブ実行可能に
- **`INSERT ... ON CONFLICT DO SELECT ... RETURNING`**: upsert で競合した行を返却できる
- **テンポラル `UPDATE` / `DELETE ... FOR PORTION OF`**: 期間（period）の部分範囲だけを更新・削除し、残りの部分は自動で分割保持。PostgreSQL 18 のテンポラル制約を補完
- **パーティション操作**: `ALTER TABLE ... MERGE PARTITIONS` / `SPLIT PARTITIONS` でインプレース再編成
- **`GROUP BY ALL`**: 非集約・非ウィンドウの出力列を自動で GROUP BY に含める

### パフォーマンス・運用

- **FK チェックありの INSERT が 約2倍高速化**
- **並列 autovacuum**: `autovacuum_max_parallel_workers` で制御
- **`REPACK` コマンド**: `CONCURRENTLY` オプションで非ブロッキングにテーブル再編成（`VACUUM FULL` の代替）
- **I/O ワーカー自動スケール**: `io_min_workers` / `io_max_workers`
- **`pg_plan_advice` / `pg_stash_advice`**: プランナーへのヒント注入フレームワーク

### 論理レプリケーション

- シーケンス値のレプリケーション（オンラインアップグレードを簡素化）
- `CREATE PUBLICATION ... EXCEPT` 構文
- `CREATE SUBSCRIPTION ... SERVER`（認証情報の管理）
- **動的有効化**: サーバー再起動不要、`wal_level = replica` で動作

### 監視・可観測性

- `pg_stat_lock` ビュー（ロック種別ごとの統計）
- `pg_stat_recovery` ビュー（リカバリ状況の可視化）
- `EXPLAIN (ANALYZE, IO)` で非同期 I/O 統計を取得
- プロセス種別ごとの `log_min_messages` 設定

### セキュリティ

- `pg_hosts.conf` による SNI サポート（ホスト名ごとに異なる TLS 証明書）
- `password_expiration_warning_threshold`（デフォルト 7日）
- `md5_password_warnings` 設定

## 破壊的変更・移行ガイド

| 設定 / 機能 | 変更内容 | 対応 |
|------------|---------|------|
| `default_toast_compression` | デフォルトが `lz4` に | pglz 前提の運用がある場合は明示指定 |
| JIT | **デフォルト無効化** | JIT に依存した分析クエリは `jit = on` を検討 |
| データチェックサム | 再起動なしでオンライン切替可能に | — |
| RADIUS 認証 | **削除** | 代替認証方式へ移行 |
| md5 認証 | deprecate（警告通知） | SCRAM-SHA-256 へ移行 |

## 今後の注目点

- Beta 期間中に、上記デフォルト変更（特に JIT 無効化と toast 圧縮）が既存ワークロードの性能に与える影響を本番相当データで検証しておくべき。
- `REPACK CONCURRENTLY` が `VACUUM FULL` / pg_repack 拡張の運用をどこまで置き換えられるか。
- GA は 9〜10月頃。追加 Beta / RC を経て確定するため、新機能の挙動は最終版で再確認すること。
