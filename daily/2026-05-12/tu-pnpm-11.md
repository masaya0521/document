# pnpm 11 — サプライチェーン防御の minimumReleaseAge と Store v11

- **日付**: 2026-05-12
- **カテゴリ**: Build Tool / Package Manager
- **ソース**:
  - [pnpm 11.0 ブログ](https://pnpm.io/blog/releases/11.0)
  - [pnpm v11.0.0 リリース (GitHub)](https://github.com/pnpm/pnpm/releases/tag/v11.0.0)
  - [Migrating from v10 to v11](https://pnpm.io/migration)
  - [InfoQ: pnpm 11 RC – ESM Distribution, Supply Chain Defaults and a New Store Format](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/)

## 概要

pnpm 11 は 2026 年 4 月末に正式リリースされ、5 月にも継続的にパッチ（11.0.6 など）が出ている。最大の特徴は「npm エコシステムで頻発するサプライチェーン攻撃を、パッケージマネージャ側のデフォルトでブロックする」方向に大きく舵を切ったこと。`minimumReleaseAge` と `blockExoticSubdeps` がデフォルトで有効になり、ストアの内部形式も SQLite ベースの Store v11 に刷新された。

ESM 化と Node.js 22+ 必須化、設定ファイルの統合など、運用面の破壊的変更も多いため、CI／開発環境のセットアップには注意が必要。

## 主な変更点

### サプライチェーン防御のデフォルト

- **`minimumReleaseAge: 1440`（1 日）がデフォルト**: 新しく publish されたバージョンは、リリースから 24 時間経過するまでインストールされない。乗っ取り直後の悪性パッケージが本番ビルドに混入するのを抑える。
- **`blockExoticSubdeps: true` がデフォルト**: 推移依存に `github:` / `git+https:` などのレジストリ外パッケージを引き込むことをブロック。
- 既存挙動を維持したい場合は `pnpm-workspace.yaml` で `minimumReleaseAge: 0` / `blockExoticSubdeps: false` を明示する。

これらは「危険性を理解した上でオプトアウトする」設計になっており、デフォルト安全側に振り切った点が大きい。

### Store v11（SQLite ベース）

旧来は `$STORE/index/` 配下に数百万件の JSON ファイルが散らばっていたが、これが単一の SQLite データベース `$STORE/index.db` に統合された。

- **MessagePack 値・WAL モード**で並行アクセス可能。
- パッケージのバンドル済みマニフェスト（name / version / bin / engines / scripts）も index に格納されるため、`package.json` を都度読みに行く syscall が消える。
- 結果として「キャッシュヒット時の依存解決＋リンクが大幅に高速化」する。

### ESM 化 & Node.js 22+ 必須

- pnpm 本体が純粋な ESM として配布されるようになり、Node.js 18 / 19 / 20 / 21 のサポートが打ち切られた。Node.js **22 以降**が必須。
- これにより内部の遅延ロードや起動時間も改善されているが、CI で古い Node を使っているプロジェクトはまず Node のバージョン更新から必要。

### ビルドスクリプト設定の統合

`onlyBuiltDependencies` / `onlyBuiltDependenciesFile` / `neverBuiltDependencies` / `ignoredBuiltDependencies` / `ignoreDepScripts` の 5 設定が **`allowBuilds` 1 つに統合**された。さらに `strictDepBuilds` がデフォルト `true` に。

ネイティブビルドが必要な依存（`esbuild`、`sharp`、`prisma` 等）は `allowBuilds` で明示的に許可するスタイルに変わる。

### SBOM 生成のビルトイン

CycloneDX / SPDX 形式の SBOM 生成が標準コマンドとして提供されるようになった。サプライチェーン監査・脆弱性スキャンとの連携が容易になる。

## 破壊的変更・移行ガイド

| 変更 | 対応 |
|------|------|
| `package.json` の `pnpm` フィールドが読まれなくなる | 設定はすべて `pnpm-workspace.yaml` に集約 |
| `.npmrc` で読まれるのは auth / registry 系のみ | `hoist-pattern` / `node-linker` / `save-exact` 等は `pnpm-workspace.yaml` に camelCase で移動 |
| ビルドスクリプト関連の 5 設定が削除 | `allowBuilds` に統合、`strictDepBuilds: true` がデフォルト |
| Node.js 18-21 サポート終了 | Node.js 22+ に更新 |

公式に **`pnpm-v10-to-v11` codemod** が用意されており、機械的な書き換えはこれで済む。残りは人間が判断するスタイル。

## 今後の注目点

- npm 本体側も `minimumReleaseAge` 相当の仕組みを検討中とされており、エコシステム全体で「即時依存」から「枯らした依存」へ移行する流れになりそう。
- 多くの OSS が `minimumReleaseAge` 起因で「最新パッチが当日反映されない」状態になるため、緊急セキュリティパッチが必要な時は明示的に `--ignore-release-age` 相当のオプションで取り込む運用が必要。
- Store v11 への移行は自動だが、複数バージョンの pnpm を併用する環境（古いプロジェクトに pnpm 10 を残す等）では、ストア互換性に注意。
