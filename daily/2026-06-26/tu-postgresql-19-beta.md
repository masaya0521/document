# PostgreSQL — 19 Beta 1 リリース

- **日付**: 2026-06-04
- **カテゴリ**: DB・Infra
- **ソース**: [PostgreSQL 19 Beta 1 Released!（公式）](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/), [PostgreSQL 19 New Features（Neon）](https://neon.com/postgresql/postgresql-19-new-features), [What's New in Postgres 19（Snowflake）](https://www.snowflake.com/en/blog/engineering/postgresql-19-features-beta/)

## 概要

PostgreSQL 19 Beta 1 が 2026 年 6 月 4 日にリリースされた。最初のベータとして全機能が出揃い、これ以降は必要に応じて追加ベータ・リリース候補（RC）を経て、最終 GA は 2026 年 9〜10 月頃が見込まれている。今回はグラフクエリの標準サポート、オンラインでのテーブル再編成、autovacuum の並列化など、運用負荷とスケーラビリティに直結する機能が多く含まれる点が特徴。

## 主な変更点

### SQL 機能

- **SQL/PGQ プロパティグラフクエリ**: SQL 標準のグラフクエリ構文をサポートし、リレーショナルデータに対するグラフ的な探索が可能に。
- **`ON CONFLICT DO SELECT`**: 競合時に既存行を返せる新構文。no-op UPDATE による回避策と比べてベンチマーク上ほぼ 4 倍高速。
- **`COPY TO` のネイティブ JSON 出力**: エクスポートを JSON 形式で直接出力可能に。
- **テンポラルデータ**: `UPDATE ... FOR PORTION OF` / `DELETE ... FOR PORTION OF` を追加し、期間指定の部分更新・削除に対応。

### 運用・パフォーマンス

- **`REPACK` コマンド**: オンラインでのテーブル再編成（再構築）を標準コマンドとして提供。
- **並列 autovacuum**: autovacuum を並列化し、大規模テーブルのメンテナンス時間を短縮。
- **オンライン checksums**: 稼働中のクラスタでデータ checksum の有効化・無効化が可能に。
- **MultiXactOffset の 64bit 化**: 従来 32bit だった MultiXactOffset を 64bit に拡張し、約 40 億メンバーのラップアラウンド上限リスクを解消。

## 破壊的変更・移行ガイド

- ベータ版のため本番利用は非推奨。新機能の検証・互換性確認を目的としたテスト環境での利用が前提。
- GA に向けてカタログ構造や挙動が変わる可能性があるため、ベータ間・RC 間でのデータ互換性は保証されない（検証用クラスタを使い捨てる運用を推奨）。
- 既存アプリケーションでは、`ON CONFLICT DO SELECT` やテンポラル構文など新 SQL の採用を見据えた事前検証が有効。

## 今後の注目点

- GA（2026 年秋見込み）までに追加されるベータ／RC での挙動変更・性能チューニング。
- SQL/PGQ によるグラフクエリが、専用グラフ DB の利用シーンをどこまで吸収できるか。
- 並列 autovacuum・`REPACK`・オンライン checksums といった「無停止運用」系機能の実運用での効果検証。
