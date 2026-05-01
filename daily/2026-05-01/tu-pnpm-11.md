# pnpm 11.0 — サプライチェーン保護がデフォルトになった大型リリース

- **日付**: 2026-05-01
- **カテゴリ**: Build Tool / Package Manager
- **ソース**: [pnpm Blog: pnpm 11.0](https://pnpm.io/blog/releases/11.0), [InfoQ: pnpm 11 Release Candidate](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/), [GitHub Releases](https://github.com/pnpm/pnpm/releases)

## 概要

pnpm 11 は v10 で導入されたセキュリティ強化のデフォルト化を中心に据えたメジャーリリース。`npm CLI` への内部委譲を廃止して publish/login/view 等を完全自前実装に切り替え、ストアフォーマットを SQLite ベースに刷新、設定の置き場所を `pnpm-workspace.yaml` に集約するなど、運用面も含めた整理が同時に進んでいる。Node.js 22 必須化と純粋 ESM 化によりエコシステム前提も大きく前進した。

## 主な変更点

### サプライチェーン保護がデフォルトに
- `minimumReleaseAge` のデフォルトが `1440`（= 24 時間）に変更され、公開直後のパッケージは自動的に保留される。
- `blockExoticSubdeps` がデフォルト `true` になり、URL/Git 等の異形依存をブロック。
- 監査機構が CVE 中心から GHSA 中心のフィルタリングに移行。`ignoreCves` は `ignoreGhsas` に置き換わる。

### ランタイム / 配布形態
- pnpm 自体が pure ESM になり、Node.js 22 以上を必須化（18〜21 のサポートは終了）。
- グローバルインストールを隔離し、ユーザー環境の global を汚染しないように。

### npm CLI への依存を解消
- `pnpm publish` / `login` / `logout` / `view` / `deprecate` / `unpublish` / `dist-tag` / `version` がいずれもネイティブ実装に。npm CLI へフォールバックしない。
- 生体認証付き 2FA など、独自実装の publish フローに置き換わる。

### ストアの再設計
- 従来パッケージごとに JSON を持っていたストアインデックスを SQLite 1 ファイルに統合（Store v11）。読み書き性能と一貫性を改善。

### 設定ファイルの整理
- pnpm 固有の設定は `pnpm-workspace.yaml` または `~/.config/pnpm/config.yaml` に集約。
- `.npmrc` は認証・レジストリ設定だけが残る。
- 環境変数も `npm_config_*` ではなく `pnpm_config_*` を読むように。
- ビルド許可関連の設定 (`onlyBuiltDependencies` / `neverBuiltDependencies` 等) は `allowBuilds` に統合。

### 新コマンド
- `pnpm ci`：lockfile に厳密に従ったクリーンインストール。
- `pnpm sbom`：SPDX/CycloneDX 形式の SBOM を出力。
- `pnpm clean`：`node_modules` を高速削除。
- `pnpm docs` / `pnpm home`：パッケージのドキュメント・ホームページをブラウザで開く。
- `pnpm ping`：レジストリへの接続確認をネイティブで実行。

## 破壊的変更・移行ガイド

| 領域 | v10 | v11 | 対応 |
|------|-----|-----|------|
| Node.js | 18 以上 | **22 以上** | Node.js 22 LTS 系へ更新 |
| 設定ファイル | `.npmrc` | `pnpm-workspace.yaml` / `~/.config/pnpm/config.yaml` | コードモッドで自動移行 |
| 環境変数 | `npm_config_*` | `pnpm_config_*` | CI/CD のシークレット名を読み替え |
| ビルド許可 | `onlyBuiltDependencies` 等 | `allowBuilds` | 既存の許可リストを統合 |
| 監査 | `ignoreCves` | `ignoreGhsas` | CVE → GHSA で書き換え |
| 配布形態 | CJS 互換 | **Pure ESM** | 古いツールで pnpm を require している場合は要対応 |

公式は `pnpm-v10-to-v11` コードモッドを提供しており、設定ファイル移行はほぼ自動化できる。最初に `pnpm setup` を再実行してシェル設定を更新し、その後コードモッドを当てる流れが推奨。

`minimumReleaseAge=1440` がデフォルト適用されることで、リリース直後のパッケージは即座にはインストールされない点に注意。緊急対応で最新版を取り込みたい場合は明示的に `--allow-new-releases` 等で外す必要がある。

## 今後の注目点

- Bun の package manager や Yarn 4 と比較した際のサプライチェーン耐性で、デフォルト設定での「安全側」ポリシーをどこまで広めにできるか。
- SQLite ストアによるモノレポ大規模環境での実測ゲイン（インストール時間・ディスク I/O）。
- pnpm 固有設定の `pnpm-workspace.yaml` 集約により、IDE/CI 側ツールがどこまで早期に追従するか。
- `pnpm sbom` がサプライチェーン関連の規制対応（SLSA, SBOM 提出義務化）にどれだけ刺さるか。
