# pnpm — 11（最新パッチ 11.5.2）

- **日付**: 2026-06-07
- **カテゴリ**: Build Tool / Package Manager
- **ソース**: [pnpm 11.0 Release Notes](https://pnpm.io/blog/releases/11.0), [pnpm Releases (GitHub)](https://github.com/pnpm/pnpm/releases), [pnpm 11 RC (InfoQ)](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/)

## 概要

pnpm 11 は、npm エコシステムで続発するサプライチェーン攻撃への防御を**デフォルトで有効化**したメジャーリリース。公開直後の悪意あるパッケージを取り込みにくくする「最小リリース経過時間（`minimumReleaseAge`）」を標準で 1 日に設定し、加えてストレージ層を SQLite ベースの **Store v11** へ刷新、配布形態を pure ESM 化した。最新パッチは 11.5.2（6/5 リリース）。

## 主な変更点

### サプライチェーン対策のデフォルト化
- `minimumReleaseAge` が **デフォルト 1440 分（1日）** に。npm に公開されてから 1 日経過していないバージョンは解決対象から除外される（typosquatting / 即時公開型マルウェアの緩和）。
- `blockExoticSubdeps` がデフォルト `true`。異常な（exotic な）サブ依存をブロックする。
- グローバルインストールが各パッケージごとに隔離され、相互干渉を排除。

### Store v11（新ストアフォーマット）
- パッケージインデックスが **単一の SQLite データベース**に。従来の数百万の JSON ファイル管理から脱却。
- バンドル済み manifest をパッケージインデックスに直接格納し、解決時の読み込みを削減。

### pure ESM 配布
- pnpm 本体が pure ESM で配布されるようになり、**Node.js 22 以降のみサポート**。Node 18〜21 のサポートは廃止。

### 設定とビルドの整理
- `allowBuilds` が従来のビルド設定（`onlyBuiltDependencies` 等）を置き換え、統一。
- `.npmrc` は認証/レジストリ設定専用に。pnpm 固有設定は `pnpm-workspace.yaml` への移行が必須。

## 破壊的変更・移行ガイド

- **Node.js 22+ が必須**: それ未満の環境では実行不可。CI / ローカルの Node バージョンを先に引き上げる。
- **設定ファイルの分離**: これまで `.npmrc` に書いていた pnpm 固有設定（`onlyBuiltDependencies` など）は `pnpm-workspace.yaml` に移す必要がある。
- **`minimumReleaseAge` の影響**: 公開直後の最新バージョンを意図的に使いたい場合（自社パッケージの即時利用など）は、`minimumReleaseAge` を 0 にするか該当パッケージを `minimumReleaseAgeExclude` 等で除外する。CI で「最新版が解決されない」事象が出たらまずこの設定を疑う。
- **ビルド許可の明示**: ポストインストールスクリプトを実行する依存は `allowBuilds` で明示的に許可する必要がある。

## 今後の注目点

- Rust 製の install バックエンド **pacquet** の段階的導入（実験的オプトイン）による高速化の進展。
- `minimumReleaseAge` デフォルト化が他のパッケージマネージャ（npm / yarn）の既定挙動に与える影響。
- Store v11（SQLite 化）による大規模 monorepo でのインストール性能・ディスク効率の実測評価。
