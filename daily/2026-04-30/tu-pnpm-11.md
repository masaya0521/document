# pnpm v11.0 — サプライチェーン防御を default に、ストアも刷新した節目のメジャーリリース

- **日付**: 2026-04-28
- **カテゴリ**: Build Tool / Package Manager
- **ソース**: [pnpm Blog: pnpm 11.0](https://pnpm.io/blog/releases/11.0), [InfoQ: pnpm 11 RC](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/), [GitHub Releases](https://github.com/pnpm/pnpm/releases)

## 概要

pnpm のメジャーバージョンとして 4/28 に v11.0 が GA。今回のリリースは「セキュリティを後付けではなく default に組み込む」「ストアフォーマットを SQLite に刷新する」「pnpm 自体を ESM 専用にする」という 3 つの基軸で、過去の v10 系から見るとかなり踏み込んだ破壊的変更を含む。Node.js のバージョン要件も 22 以上に引き上げられ、ESM 化や設定ファイルの再編成と合わせて、CI／開発者環境の両方に「アップグレード前に対応すべき項目」が複数ある節目のリリースとなる。

公式には `pnpm-v10-to-v11` という codemod が提供され、`.npmrc` から `pnpm-workspace.yaml` への設定移行など定型作業はほぼ自動化できる。とはいえ minimumReleaseAge による新規パッケージ取り込みの遅延は意図的に挙動を変えるオプションのため、CI／公開フロー側のレビューがセットで必要になる。

## 主な変更点

### サプライチェーン保護をデフォルト ON

- `minimumReleaseAge` のデフォルトが 1440（分）= 1 日に変更。npm に publish された直後の新バージョンは、ローカル／CI のインストール対象として 1 日待ってから採用されるようになり、汚染パッケージがマージされる前にコミュニティが気付くまでの「冷却期間」が default で挿入される。
- `blockExoticSubdeps` のデフォルトが `true`。git URL や tarball URL など `npm:` 以外のサブ依存を、明示的な許可なしには引き込まないようブロックする。
- 効果: postinstall script による典型的なサプライチェーン攻撃に対して、レジストリと依存形態の両方からデフォルトで一段ガードがかかる構成になった。

### ストアフォーマットを SQLite に刷新（Store v11）

- 旧来の「パッケージごとに JSON ファイル」を散在させていたインデックスを、`store.db` という単一の SQLite データベースに統合。
- 数百万ファイル単位の小ファイル I/O が消え、`pnpm install` の cold-cache でのスループットと、CI 上の monorepo でのパフォーマンスが大幅に改善。
- 既存ストアからの自動マイグレーションが入っており、初回 install 時に新フォーマットに変換される。

### Node.js 22+ 必須・pnpm 本体は pure ESM

- Node.js 18 / 19 / 20 / 21 のサポートを drop。pnpm 自体のコードベースが pure ESM になっており、CommonJS ローダー経由の require は不可。
- スタンドアロンバイナリ側も glibc 2.27 以上が要件。古い CI ランナー（古い Ubuntu 20.04 以前のベースイメージ等）では先にイメージ更新が必要。

### 設定ファイルの再編成

- `.npmrc` は **認証・レジストリ設定専用** に絞られる（INI 形式）。
- pnpm 固有の挙動設定は `pnpm-workspace.yaml` に集約（YAML 形式）。`onlyBuiltDependencies`, `auditConfig.ignoreCves`, `packageExtensions` などはこちらに移動。
- グローバル設定は `~/.config/pnpm/config.yaml` に統一。
- 環境変数のプレフィックスは `pnpm_config_*` に統一。
- `onlyBuiltDependencies` 等のビルド許可制御は `allowBuilds` マップに統合され、postinstall script の許可ポリシーをひとつのオブジェクトで管理できるようになった。

### Publish / npm CLI への依存を排除

- `pnpm publish`, `login`, `logout`, `view`, `deprecate`, `unpublish`, `dist-tag`, `version` がネイティブ実装になり、内部で `npm` CLI を呼び出すフォールバックが廃止。
- 認証フローやエラーハンドリングが pnpm 側で一貫し、レジストリの 2FA や OIDC を含む CI からの publish が pnpm のみで完結する。

### グローバルインストールの隔離

- `pnpm add -g` で入れたパッケージごとに独立した依存ディレクトリを持つ構成に変更。あるグローバルツールが他のグローバルツールの依存を間接的に上書きする問題が解消。

## 破壊的変更・移行ガイド

`pnpm-v10-to-v11` codemod が公式提供されているので、まずはこれを実行するのが基本。手動で確認すべきポイントは以下。

1. **Node.js のアップグレード**: CI のランナーイメージ／Docker ベースイメージで Node 22+ になっているか確認。古い Alpine / Ubuntu ベースで glibc バージョンが不足していないかも要確認。
2. **設定ファイルの分割**: 既存 `.npmrc` の中で `auto-install-peers`, `node-linker`, `prefer-frozen-lockfile`, `auditConfig.*` 等の pnpm 固有設定がある場合、それらを `pnpm-workspace.yaml` 側に移す。`.npmrc` には registry / auth token 系のみ残す。
3. **環境変数のリネーム**: `NPM_CONFIG_*` で pnpm の挙動を制御していた CI 設定がある場合、`pnpm_config_*` に置き換える。
4. **`minimumReleaseAge` の運用判断**: デフォルト 1 日の遅延を許容できないユースケース（自社製パッケージを公開直後にすぐインストールしたい場合など）は、当該パッケージのみ `minimumReleaseAgeExclude` で除外するか、CI 側で値を 0 に設定する。安全側のデフォルトは維持しつつ自社パッケージだけ除外、が推奨パターン。
5. **`blockExoticSubdeps`**: git URL / tarball URL を間接依存として引いているライブラリ（私有 fork や monorepo 内の workspace: 参照ではないもの）がある場合、明示的に許可リストに加える必要がある。`pnpm install` がここで失敗するケースが多いので、まずはローカルで試走すべし。
6. **publish フローの差分確認**: `pnpm publish` を CI で使っている場合、内部実装が変わっているのでドライラン（`--dry-run`）で 2FA / OIDC / provenance 周りに差分が出ないかを確認。
7. **ストア再作成**: 既存ストアは自動マイグレーションされるが、必要に応じて `pnpm store path` を確認したうえで一度クリアして再構築するとサイズが減るケースがある。

## 今後の注目点

- `minimumReleaseAge` のデフォルト ON は、エコシステム全体としても「新パッケージのインストールに 1 日の冷却期間を置く」が標準になり得るかどうかの試金石。Yarn / npm 側がこれに追随するか注視。
- ストアの SQLite 化はパッケージマネージャ全般のトレンドになりうる。Bun の install ストアや、Rolldown / Turbopack 系の依存解決にも波及するか。
- pnpm 自体の pure ESM 化は、Node.js エコシステムの ESM-first シフトをさらに加速させる。`require()` で import していたツールチェーンの内部参照が壊れるケースがあるため、プラグインやレシピ系の生態系も追従が必要。
- 次の v11.x マイナーで、`allowBuilds` の policy DSL がさらに表現力を増す方向の議論が進んでいる。postinstall script を「明示的に許可した依存のみ」しか実行しないという pnpm の方向性は今後も強化されていきそう。
