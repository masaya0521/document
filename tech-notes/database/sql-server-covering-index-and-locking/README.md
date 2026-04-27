# SQL Server: カバリングインデックスとロック方式の基礎

- **日付**: 2026-04-27
- **カテゴリ**: Database / SQL Server / Performance / Concurrency

「最新版ポインタ」のような単純な引きクエリを設計するときに、`INCLUDE` の使い方と排他制御の選択（楽観 / 悲観）で迷うことが多い。両者は設計時に同時に考えておくと、後から「やっぱりこのカラム必要だった」「ロック方式を変えるならインデックスも見直しが要る」という手戻りが減る。本ノートでは両者を一気通貫で整理する。

---

## 1. 非クラスタ化インデックスの基本構造

SQL Server のテーブルには 2 種類のインデックスがある。

### クラスタ化インデックス（Clustered Index）

- テーブルの**物理的な並び順そのもの**
- リーフページに**全カラム**が格納される（= テーブルの本体）
- 1 テーブルに 1 つだけ
- 通常は `PRIMARY KEY` がこれになる

### 非クラスタ化インデックス（Nonclustered Index）

- 別構造で作られる B-tree
- リーフページには **インデックスキー + クラスタ化インデックスのキー（=PK、または heap の RID）** が入る
- 1 テーブルに複数作成可能

例として以下のテーブルを考える:

```sql
CREATE TABLE article_latest (
    article_id   int          NOT NULL PRIMARY KEY,  -- クラスタ化 PK
    author_id    int          NOT NULL,
    revision_no  int          NOT NULL,
    updated_at   datetime2(7) NOT NULL,
    row_version  rowversion   NOT NULL
)
CREATE UNIQUE NONCLUSTERED INDEX UQ_article_latest_author_id
    ON article_latest (author_id)
```

非クラスタ化インデックス `UQ_article_latest_author_id` のリーフページに格納されるのは:

```
[author_id (キー), article_id (PK が暗黙的に含まれる)]
```

つまり、**インデックスキーと PK 以外のカラム（`revision_no`, `updated_at`, `row_version`）はリーフに入っていない**。

---

## 2. Key Lookup の発生

`author_id` で検索して `revision_no` も取得したい:

```sql
SELECT article_id, revision_no
FROM article_latest
WHERE author_id = 12345
```

このクエリの実行計画は以下の 2 ステップ:

1. **Index Seek**: `UQ_article_latest_author_id` のリーフから `(author_id=12345, article_id=789)` を取得
2. **Key Lookup**: `revision_no` を取るためにクラスタ化インデックス（`article_id` PK）に飛ぶ

Key Lookup は「**インデックスに乗っていないカラムを引きに行く**」処理。1 行ならコストは小さいが、リスト系クエリで何百行もスキャンすると I/O が積み上がる。

実行計画を見ると `Key Lookup (Clustered)` というオペレータが現れる。SQL Server Management Studio で「実行プランの表示」を有効にすると視覚的に確認できる。

---

## 3. `INCLUDE` でカバリングインデックスにする

`INCLUDE` 句は「**インデックスのリーフページに、検索対象ではないカラムを追加で格納する**」指示。

```sql
CREATE UNIQUE NONCLUSTERED INDEX UQ_article_latest_author_id
    ON article_latest (author_id)
    INCLUDE (article_id, revision_no)
```

これでリーフページの内容が:

```
[author_id (キー), article_id, revision_no]
                    ↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑
                    INCLUDE で追加された
```

先ほどの `SELECT article_id, revision_no FROM ... WHERE author_id = 12345` は、**インデックスのリーフを引くだけで全カラム揃う**ので Key Lookup なしで完結する。これを **カバリングインデックス（covering index）** と呼ぶ。

### キー列と INCLUDE 列の違い

| 観点 | インデックスキー（`(author_id)` の部分） | INCLUDE 列 |
|---|---|---|
| ソート対象 | ✅ B-tree の階層構造に含まれる | ✗ リーフのみ |
| 検索条件に使える | ✅ `WHERE` / `JOIN` / `ORDER BY` の対象 | ✗ 取得用のみ |
| range scan / seek | ✅ | ✗ |
| インデックスサイズへの影響 | 大（B-tree のノードに乗る） | 中（リーフのみ） |
| キー列の制限（900 byte / 1700 byte） | あり | 制限が緩い（最大 column 数の制限のみ） |

原則: **検索したいカラムはキーに、結果として欲しいだけのカラムは INCLUDE に**。

### INCLUDE が向くカラム

- 検索条件には使わないが、SELECT 句で頻繁に取得される
- データサイズが小さめ（巨大な BLOB 列を INCLUDE するとリーフが膨らむ）
- 値が頻繁に変わるカラムは UPDATE コストに注意（インデックスも更新される）

### INCLUDE のサイズ感

Key Lookup を回避するメリットは大きいが、INCLUDE 列が多すぎるとインデックス自体が肥大化して効率が落ちる。目安として:

- **1〜3 列程度を INCLUDE** するのが一般的
- 各列が 8 バイト程度なら、行数 100 万に対して INCLUDE 1 列で +8 MB 程度（実用上ほぼ無視できる）
- 文字列や JSON など可変長で大きいカラムは慎重に

---

## 4. 楽観排他制御 vs 悲観排他制御

「最新版ポインタ」のような行を更新する設計では、複数のリクエストが同時に同じ行を更新しようとしたときの競合をどう防ぐかを決める必要がある。SQL Server では大きく 2 つの方式がある。

### 楽観排他制御（Optimistic Concurrency Control）

「衝突しないだろう」と楽観してロックを取らずに進め、**更新時に衝突を検知**する方式。

#### `rowversion` 型を使った典型例

`rowversion`（旧名 `timestamp`）は **行が更新されるたびに 8 バイトの値が自動的に変わる** SQL Server 独自の型。これを使った楽観制御:

```sql
-- 1. 読み込み時に row_version を取得
SELECT article_id, revision_no, row_version
FROM article_latest
WHERE author_id = 12345

-- ... アプリ層で処理 ...

-- 2. 更新時に「読み込み時の row_version と一致する」ことを条件にする
UPDATE article_latest
SET revision_no = ?, updated_at = SYSUTCDATETIME()
WHERE article_id = ? AND row_version = @original_row_version

-- 3. @@ROWCOUNT を確認
IF @@ROWCOUNT = 0
    -- 他プロセスが先に更新した → エラー or リトライ
```

`@@ROWCOUNT = 0` なら衝突が起きたと判定。アプリ層で「やり直すか、エラーにするか」を決める。

#### メリット・デメリット

| 観点 | 評価 |
|---|---|
| 読み込み時の負荷 | ✅ ロック不要、軽い |
| 同時実行数が多い場合 | ✅ ブロッキングしない |
| 衝突時のコスト | ✗ アプリ層でリトライ実装が必要 |
| 衝突頻度が高い場合 | ✗ リトライ地獄になりうる |

### 悲観排他制御（Pessimistic Concurrency Control）

「衝突するかもしれない」と悲観して、**最初から行ロックを取って他プロセスを待機させる**方式。

#### `WITH (UPDLOCK, ROWLOCK)` を使った典型例

```sql
BEGIN TRAN
  -- 1. SELECT 時点で行ロックを取る（更新ロック + 行レベル）
  DECLARE @current_revision int = (
    SELECT revision_no
    FROM article_latest WITH (UPDLOCK, ROWLOCK)
    WHERE author_id = 12345
  )

  -- 2. 計算など
  DECLARE @new_revision int = @current_revision + 1

  -- 3. UPDATE（同トランザクション内なのでロックは継続）
  UPDATE article_latest
  SET revision_no = @new_revision, updated_at = SYSUTCDATETIME()
  WHERE author_id = 12345
COMMIT
```

`UPDLOCK` ヒントで、SELECT した時点から更新ロックを取得。トランザクション完了まで他プロセスからの同行に対する `UPDLOCK` 取得が**待機**する（共有ロックは取れる）。

#### よく使う SQL Server のロックヒント

| ヒント | 意味 |
|---|---|
| `UPDLOCK` | 更新ロックを取る（後で UPDATE する前提の SELECT） |
| `HOLDLOCK` | トランザクション完了まで共有ロックを保持（≒ SERIALIZABLE 相当） |
| `ROWLOCK` | 行レベルでロック（ページロックや表ロックへのエスカレーションを抑制） |
| `XLOCK` | 排他ロックを直接取る（共有ロックも取れない） |
| `READPAST` | ロックされた行をスキップ |
| `NOWAIT` | ロック待機せず即座にエラーを返す |

組み合わせの定番:

- `WITH (UPDLOCK, ROWLOCK)`: 「これから UPDATE する 1 行をロック」
- `WITH (UPDLOCK, HOLDLOCK)`: より厳密に、phantom も防ぐ（SERIALIZABLE 相当）
- `WITH (NOLOCK)`: ロック取らずダーティリード許容（⚠️ 整合性が必要な処理では使わない）

#### メリット・デメリット

| 観点 | 評価 |
|---|---|
| 衝突時のコスト | ✅ 自動的に待機、リトライ実装不要 |
| 実装の素直さ | ✅ アプリ層がシンプル |
| 同時実行数が多い場合 | ✗ ブロッキングが発生 |
| デッドロック | ✗ 順序を間違えると 1205 エラーが起きうる |

---

## 5. どちらを選ぶか

### 楽観が向くケース

- **読み込みが多く、更新頻度が低い**: ブロッキングコストを払いたくない
- **長時間のトランザクション**: 読み込み中ずっとロックを保持したくない
- **Web アプリの「画面表示 → 編集 → 保存」**: 編集中にロックを保持し続けるのは現実的でない
- **競合がレア**: リトライがほぼ起きないので楽観が軽い

### 悲観が向くケース

- **同時更新が起きる経路が複数あり、競合が読みにくい**
- **採番や一意性チェックを伴う更新**: 確実に衝突を防ぎたい
- **短時間で完結する書き込み**: ロック保持時間が短い
- **アプリ層でリトライを書きたくない**: 実装の素直さ重視

### 両方併用も可能

楽観の `rowversion` 比較と悲観の `UPDLOCK` を併用すると、

- 通常はロックで防ぐ
- 万が一の漏れを `rowversion` で事後検知

という「保険」付きの設計になる。コストは `rowversion` カラム 8 バイト × 行数程度。実用上ほぼ無視できる。

---

## 6. INCLUDE と排他制御の関係

設計時に両者を一緒に考えるべき理由は、**楽観制御を選ぶなら `rowversion` を読みたくなる**ため。

### 楽観制御を採用する場合

`SELECT ... WHERE 自然キー = ?` で `rowversion` も同時に取得したい:

```sql
SELECT article_id, revision_no, row_version
FROM article_latest
WHERE author_id = ?
```

この経路を Key Lookup なしで引きたいなら、`INCLUDE` に `rowversion` を含める:

```sql
CREATE UNIQUE NONCLUSTERED INDEX UQ_article_latest_author_id
    ON article_latest (author_id)
    INCLUDE (article_id, revision_no, row_version)
                                       ^^^^^^^^^^^
                                       楽観制御で必要
```

### 悲観制御を採用する場合

`UPDLOCK` で行ロックを取るので `rowversion` は読まない。よって `INCLUDE` には不要:

```sql
CREATE UNIQUE NONCLUSTERED INDEX UQ_article_latest_author_id
    ON article_latest (author_id)
    INCLUDE (article_id, revision_no)
    -- row_version は不要
```

### 後から拡張する余地

`rowversion` 列はそもそも 8 バイトと小さいので、**「将来楽観制御に切り替えるかも」と思うなら最初から INCLUDE しておく**のもあり。インデックスの再作成は必要だが、コストは小さい。

---

## 7. 実装時の実用ポイント

### 1. デッドロック対策

悲観制御を複数経路で使う場合、**ロック取得順序を統一する**。

例えば「ユーザー → 記事」の順で常にロックを取る、と決めておけば、別経路で「記事 → ユーザー」とロックを取ることがなくなり、デッドロックが起きない。

デッドロックが起きた場合 SQL Server は自動的に片方を犠牲（victim）として 1205 エラーを返す。アプリ層で 1205 をキャッチしてリトライする実装が定石。

### 2. ロックエスカレーション

行レベルロックが多くなりすぎると、SQL Server は自動的に **ページロック / 表ロックにエスカレーション**することがある（既定で約 5000 行）。意図せず広範囲のブロッキングが起きないよう、`ROWLOCK` ヒントで明示的に行レベル維持を指定するのが安全策。

### 3. インデックスのメンテナンスコスト

INCLUDE 列を増やすと:

- INSERT / UPDATE の I/O 増（インデックスにも書き込み）
- インデックスの断片化が進みやすい

書き込みが頻繁なテーブルでは「INCLUDE は本当に必要なものだけ」が原則。

### 4. SQL Server Management Studio の実行プラン確認

設計が正しく効いているかは実行プランで確認するのが確実:

- `SET STATISTICS IO ON; SET STATISTICS TIME ON;` で I/O / 時間を計測
- 「実行プランの表示」で `Key Lookup` が消えているか視覚的に確認
- 想定通り Index Seek だけで完結していれば OK

---

## 8. 参考リンク

- [Microsoft Docs: CREATE INDEX (Transact-SQL)](https://learn.microsoft.com/en-us/sql/t-sql/statements/create-index-transact-sql)
- [Microsoft Docs: Table Hints (Transact-SQL)](https://learn.microsoft.com/en-us/sql/t-sql/queries/hints-transact-sql-table)
- [Microsoft Docs: Lock Modes](https://learn.microsoft.com/en-us/sql/relational-databases/sql-server-transaction-locking-and-row-versioning-guide)
- [Microsoft Docs: Deadlocks Guide](https://learn.microsoft.com/en-us/sql/relational-databases/sql-server-transaction-locking-and-row-versioning-guide#deadlocks)
