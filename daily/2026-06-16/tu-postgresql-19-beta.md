# PostgreSQL — 19 Beta 1 リリース

- **日付**: 2026-06-04（採録日: 2026-06-16）
- **カテゴリ**: DB・Infra
- **ソース**: [PostgreSQL: PostgreSQL 19 Beta 1 Released!](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/), [Bytebase: PostgreSQL 19 features I'm excited about](https://www.bytebase.com/blog/postgres-19-features-im-excited-about/), [Neon: PostgreSQL 19 New Features](https://neon.com/postgresql/postgresql-19-new-features)

## 概要

PostgreSQL 19 Beta 1 が 2026 年 6 月 4 日にリリースされた。PostgreSQL 18 から 200 を超える変更を含み、パフォーマンス・開発者体験・セキュリティ・モニタリング・クエリ機能の各領域にわたる改善が入っている。今後、必要に応じて追加の Beta と 1 本以上の RC を経て、**正式版（GA）は 2026 年秋（9〜10 月）頃** が見込まれる。

本リリースは「運用のしやすさ（autovacuum の並列化・観測性）」「メンテナンス作業の非ブロッキング化（REPACK）」「新しいクエリパラダイム（プロパティグラフ・時相テーブル）」が大きな柱となっている。

## 主な変更点

### パラレル autovacuum

- autovacuum が **複数のワーカーで並列実行**できるように（`autovacuum_max_parallel_workers`）。
- 大規模テーブルのバキューム時間短縮が期待でき、autovacuum の挙動も従来より観測しやすくなった。

### REPACK コマンド

- `VACUUM FULL` と `CLUSTER` を統合する新コマンド `REPACK` を追加。
- **読み書きを継続しながらテーブルを再編成できる concurrent バリアント**を備え、これまで `pg_repack` 拡張に頼っていた非ブロッキングなテーブル再構成を標準機能で実現。

### SQL/PGQ プロパティグラフクエリ

- SQL 標準の **SQL/PGQ（Property Graph Queries）** に対応。リレーショナルテーブルをグラフとして問い合わせるネイティブ構文を導入。

### 時相データ操作（FOR PORTION OF）

- `FOR PORTION OF` / `DELETE ... FOR PORTION OF` による**時相データ操作**をサポート。特定の時間範囲のデータを更新・削除する際、PostgreSQL が行を自動分割して範囲外の部分を保持する。

### 運用・観測性の強化

- 新ビュー `pg_stat_lock`（ロック種別の統計）、`pg_stat_recovery`（スタンバイ監視）を追加。`pg_stat_progress_vacuum` に動作モード詳細を追加。
- **オンラインでのチェックサム切替**（クラスタを停止せずにデータチェックサムの有効/無効を切替）。
- **MultiXact の上限撤廃**: MultiXact メンバーポインタを 32 ビットから 64 ビットへ拡張し、枯渇による上限を解消。

### 開発者体験

- **`pg_plan_advice`**: アプリを変更せずにクエリ最適化のヒントを注入できるプランナアドバイザ基盤。queryId をキーに advice をスタッシュへ保存可能。
- **DDL 抽出関数**: `pg_get_database_ddl()` / `pg_get_role_ddl()` / `pg_get_tablespace_ddl()` を追加し、カタログから CREATE 文をテキストで取得できる。
- **論理レプリケーションでのシーケンス同期**: パブリケーションがシーケンスをサポートし、フェイルオーバー時の主キー衝突を防止。
- そのほか `ON CONFLICT DO SELECT`、`COPY TO` の JSON 出力、レプリカでの陳腐な読み取りを止める `WAIT FOR LSN`、外部キー性能の改善（報道では約 2 倍）なども伝えられている。

## 破壊的変更・移行ガイド

- Beta であり本番利用は非推奨。検証は**新規環境での `pg_dump` / `pg_restore` または論理レプリケーションでの試行**を推奨。
- GA までに動作・構文が変わる可能性があるため、新クエリ機能（SQL/PGQ・`FOR PORTION OF`）の評価は GA に向けたフィードバック前提で行うこと。

## 今後の注目点

- GA（2026 年秋）に向けた追加 Beta / RC でのフィードバック反映状況。
- パラレル autovacuum と `REPACK` による大規模 DB の運用負荷低減効果の実測。
- SQL/PGQ プロパティグラフが既存のグラフ DB ワークロードをどこまで吸収できるか。
