# PostgreSQL 18 — 非同期 I/O と開発者向け新機能

- **日付**: 2026-05-11
- **カテゴリ**: DB・Infra
- **ソース**: [PostgreSQL 18 Released!](https://www.postgresql.org/about/news/postgresql-18-released-3142/), [リリースノート](https://www.postgresql.org/docs/release/18.0/)

## 概要

PostgreSQL 18 は、新しい非同期 I/O (AIO) サブシステムを中心とした大幅なパフォーマンス改善と、virtual generated columns・uuidv7()・temporal constraints などの開発者向け機能を搭載したメジャーリリース。メジャーバージョンアップグレードの高速化・安定化も注目点で、運用面での改善も大きい。

## 主な変更点

### パフォーマンス

- **非同期 I/O (AIO) サブシステム**: 複数の I/O 要求を同時発行し、sequential scan、bitmap heap scan、vacuum 等で最大 **3倍** のパフォーマンス向上。`io_method` パラメータで `worker`（デフォルト）、`io_uring`（Linux）、`sync` を切替可能
- **スキップスキャン**: マルチカラム B-tree インデックスで先頭列の条件を省略したクエリでもインデックスを活用可能に
- **FULL OUTER JOIN / RIGHT OUTER JOIN の並列実行**: クエリプランナーが複数ワーカーで分割実行
- **OR 条件のインデックス活用改善**: WHERE 句の OR 条件でより多くのケースでインデックスを使用
- **PG_UNICODE_FAST 照合順序**: `upper`/`lower`/`casefold` の高速化と完全な Unicode セマンティクス

### 開発者向け機能

- **Virtual Generated Columns**: クエリ時に値を計算する仮想生成列。ストレージを消費せず、デフォルトのオプションに
- **uuidv7()**: タイムスタンプ順序の UUID を生成する組み込み関数。インデックスの局所性が向上し、読み取りパフォーマンスが改善
- **Temporal Constraints**: 時間範囲の制約を PRIMARY KEY (`WITHOUT OVERLAPS`)、FOREIGN KEY (`PERIOD`) で定義可能
- **OLD/NEW の RETURNING 対応**: INSERT / UPDATE / DELETE / MERGE の RETURNING 句で変更前後の値を取得

### セキュリティ・認証

- **OAuth 2.0 認証**: SSO システムとの統合を簡素化。PostgreSQL 拡張機能を通じて OAuth 2.0 メカニズムに対応
- **FIPS モード検証**: FIPS 準拠環境での動作を検証するサポートを追加
- **TLS v1.3 暗号スイート設定**: `ssl_tls13_ciphers` パラメータでサーバーサイドの暗号スイートを指定可能
- **MD5 認証の廃止予告**: 将来のリリースで MD5 認証を廃止。SHA-2 ベースのパスワードハッシュを推奨

### アップグレード改善

- **プランナー統計の保持**: メジャーバージョンアップグレード時に統計情報を引き継ぎ、アップグレード直後のパフォーマンス低下を軽減
- **pg_upgrade の並列処理**: アップグレード処理自体の高速化とファイル交換機能

## 破壊的変更・移行ガイド

- `MD5` 認証は廃止予告。`scram-sha-256` への移行を推奨（`pg_hba.conf` の `md5` → `scram-sha-256`）
- `io_method` のデフォルトは `worker`。Linux 環境で `io_uring` を使う場合は明示的に設定が必要
- Virtual generated columns がデフォルトになったため、`GENERATED ALWAYS AS ... STORED` を明示しない場合は仮想列になる

## 今後の注目点

- AIO サブシステムのカバー範囲拡大（WAL write 等への適用）
- `io_uring` の安定化とデフォルト化の可能性
- temporal constraints を活用した bitemporal データモデリングの普及
- PostgreSQL 19 での MD5 認証完全廃止
