# PostgreSQL — 19 Beta 1

- **日付**: 2026-06-22
- **カテゴリ**: DB・Infra
- **ソース**: [公式ニュース（19 Beta 1 Released!）](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/), [Release 19 ドキュメント](https://www.postgresql.org/docs/19/release-19.html)

## 概要

PostgreSQL 19 Beta 1 が 2026年6月4日 にリリースされた。PostgreSQL 18 から **200以上の変更** を含み、性能・開発者体験・セキュリティ・モニタリング・クエリ機能の各面で改善が入る。今後、必要に応じて追加 Beta、続いて RC を経て、**正式リリースは2026年9〜10月頃** を予定している。Beta 段階のため本番投入は非推奨だが、機能評価・互換性検証を始めるのに適したタイミング。

## 主な変更点

### クエリ機能

- **SQL/PGQ プロパティグラフクエリ**: 標準 SQL のプロパティグラフクエリに対応
- **`ON CONFLICT DO SELECT`**: UPSERT 系の柔軟性向上
- **`REPACK` コマンド**: テーブル再編成を行う新コマンド
- **`COPY TO` のネイティブ JSON 出力**

### パフォーマンス

- **外部キーチェックの2倍高速化**: 制約検証アルゴリズムの最適化により、外部キーチェックが最大2倍高速に
- **非同期 I/O 強化**: `io_method=worker` が新しい `io_min_workers` / `io_max_workers` 設定に基づき I/O ワーカー数を自動スケール
- **`default_toast_compression` のデフォルトが lz4 に**: デフォルトの圧縮・伸長性能が向上
- **JIT がデフォルト無効化**: Just-in-time コンパイルがデフォルトで無効に

### Vacuum / 運用

- **並列 autovacuum**: autovacuum が並列ワーカーを使用可能（`autovacuum_max_parallel_workers` で設定）
- **autovacuum スコアリング**: vacuum 優先度を判定する新スコアリング機構
- **データチェックサムのオンライン切替**: クラスタ再起動や再初期化なしでチェックサムの有効/無効を切替可能

### プランナ制御

- **`pg_plan_advice` 拡張**: プランナの判断を安定化・制御できる
- **`pg_stash_advice`**: クエリ識別子を使ってアドバイスを自動適用

## 破壊的変更・移行ガイド

- **JIT デフォルト無効化**: JIT を前提にした分析ワークロードでは、必要に応じて `jit = on` を明示する
- **TOAST 圧縮のデフォルト変更（pglz → lz4）**: 圧縮形式が変わるため、ストレージ特性やレプリケーション互換性を検証する
- Beta 版のため、本番クラスタへの適用は GA 後を推奨

## 今後の注目点

- 追加 Beta / RC を経て **2026年9〜10月** に正式リリース見込み
- SQL/PGQ（プロパティグラフ）の実用度とパフォーマンス
- 並列 autovacuum・非同期 I/O の自動スケールが大規模ワークロードでどの程度効くか
- `pg_plan_advice` によるプラン安定化がプロダクション運用に与える影響
