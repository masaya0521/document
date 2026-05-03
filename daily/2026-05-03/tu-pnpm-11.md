# pnpm 11.0 — SQLite ストア・ESM 化・サプライチェーン保護のデフォルト ON

- **日付**: 2026-04-28
- **カテゴリ**: Build Tool（Package Manager）
- **ソース**: [pnpm Blog — pnpm 11.0](https://pnpm.io/blog/releases/11.0) / [InfoQ](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/) / [Migration Guide](https://pnpm.io/11.x/migration)

## 概要

pnpm 11 は 2026-04-28 にリリースされたメジャーバージョン。表面的な機能追加よりも、**ストアフォーマット、CLI ランタイム、デフォルト設定** にわたる構造的な刷新が中心となっている。最大のポイントは「JSON ファイルの集合体だったパッケージインデックスを単一の SQLite データベースに置き換えた」こと、「pnpm 自体が pure ESM になり Node.js 22+ を要求するようになった」こと、そして「サプライチェーン攻撃を念頭に置いたデフォルト値の引き締め」の 3 点。

これにより、pnpm はもはや「npm CLI の薄いラッパー」ではなくなった。`publish`・`login`・`deprecate` などこれまで npm CLI に委譲していたコマンドもネイティブ実装に置き換わっている。

## 主な変更点

### 1. ストアフォーマット: JSON → SQLite

これまで pnpm のグローバルストアは「パッケージごとに JSON のインデックスファイルを持つ」構造で、巨大な monorepo ではファイル数とメモリ消費が問題になっていた。11 ではインデックス全体を 1 個の SQLite データベースに集約。

- I/O 回数の劇的な削減
- ロック競合の解消
- ストア整合性チェックの高速化

旧フォーマットからの移行はオンデマンドで自動実行される。

### 2. ネイティブ publish フロー

- `pnpm publish` / `pnpm login` / `pnpm deprecate` が独自実装に
- npm CLI を別途インストールしておく必要がなくなる
- 認証・OTP・provenance なども pnpm 内で完結

### 3. ESM 化と Node.js 22+ 必須

pnpm 本体が pure ESM に。
- Node.js 18 / 20 / 21 サポート終了
- Node.js 22 LTS 以降が必須

CI イメージや Docker のベースイメージは更新が必要。

### 4. サプライチェーン保護のデフォルト ON

新規公開直後のパッケージを誤ってインストールするリスクを下げる方向に倒した。

| 設定 | デフォルト | 効果 |
|---|---|---|
| `minimumReleaseAge` | `1440`（分 = 1日） | 公開から 24h 経過していないバージョンはインストール対象から除外 |
| `blockExoticSubdeps` | `true` | tarball / git URL 等の非標準サブ依存をブロック |

CI で「公開直後の悪意あるバージョン」を踏むリスクを大きく下げられる一方、「リリース直後に CI を回したい」フローでは明示的なオプトアウトが必要になる。

### 5. グローバルインストールの分離

`pnpm add -g` が**インストールごとに独立したディレクトリ**を持つように。グローバル CLI 同士の依存衝突が解消される。

### 6. `.npmrc` のスコープ縮小

`.npmrc` は**認証とレジストリ設定のみ** が読まれるようになった。
- ビルド設定・hoist 設定・peer 設定などは `pnpm-workspace.yaml` または `~/.config/pnpm/config.yaml` に集約
- レポジトリの設定が散らばらず、明示的な pnpm 設定ファイルに統一される方向

### 7. ビルド設定の統合（`allowBuilds`）

`onlyBuiltDependencies` / `neverBuiltDependencies` などに散らばっていたビルド許可設定が、新しい `allowBuilds` マップに統合された。

```yaml
# pnpm-workspace.yaml
allowBuilds:
  esbuild: true
  sharp: true
  '@swc/core': false
```

### 8. その他のパフォーマンス改善

- HTTP クライアントを undici に統一
- メモリ事前割り当てによる確保コストの削減
- インストール経路全体での最適化

## 破壊的変更・移行ガイド

| 項目 | 旧 | 新 / 対応 |
|---|---|---|
| Node.js | 18 / 20 / 21 / 22 | **22+ 必須** |
| pnpm 本体 | CommonJS 互換 | **pure ESM** |
| `publish` 系 | npm CLI に委譲 | **ネイティブ実装** |
| `.npmrc` | 多目的 | 認証・レジストリのみ |
| ビルド許可 | `onlyBuiltDependencies` ほか | **`allowBuilds`** |
| グローバル | 共有ディレクトリ | **インストール毎に分離** |
| 公開直後パッケージ | 即インストール可能 | **24h 経過必須**（`minimumReleaseAge=1440`） |
| 非標準サブ依存 | 許可 | **ブロック**（`blockExoticSubdeps=true`） |

### 推奨される移行手順

1. CI / 開発環境の Node.js を 22+ にバンプ
2. `pnpm-workspace.yaml` に既存の `.npmrc` 由来設定を移送
3. `onlyBuiltDependencies` / `neverBuiltDependencies` を `allowBuilds` に書き換え
4. `pnpm install` を実行 → ストアの SQLite 移行が走る
5. CI 上で「公開直後バージョンが必要な依存」がある場合は `minimumReleaseAge` を一時的に下げるか個別に `--allow-recent` を使う

## 今後の注目点

- **競合への影響**: npm / yarn が JSON ストア + npm CLI 委譲を続けるなか、pnpm は「自前で完結する高速・安全なパッケージマネージャ」というポジションを強めた。Bun との競争関係も注視
- **モノレポでの効果検証**: 数千パッケージ規模の monorepo で SQLite ストアがどの程度のインストール時間短縮に効くか、エコシステム側からのベンチマーク報告
- **`minimumReleaseAge` のエコシステム反応**: 公開直後の即時インストールを前提にしていた CI / リリース系ツールがどう適応するか
- **provenance / SBOM 連携**: ネイティブ publish が provenance や SBOM 出力をどこまで取り込んでいくか
