# pnpm 11 — サプライチェーン防御デフォルト ON と SQLite ストア

- **日付**: 2026-04-28
- **カテゴリ**: Build Tool / Package Manager
- **ソース**: [pnpm 11.0 Blog](https://pnpm.io/blog/releases/11.0), [Migration v10 → v11](https://pnpm.io/11.x/migration), [InfoQ: pnpm 11 RC](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/), [GitHub Release](https://github.com/pnpm/pnpm/releases/tag/v11.0.0)

## 概要

pnpm のメジャーバージョン 11 がリリース。マイナー追加というよりは「**安全側に倒したデフォルト**」と「**ストア構造の刷新**」をまとめて投入したアップグレード。
特にサプライチェーン攻撃の流行を受けて `minimumReleaseAge` と `blockExoticSubdeps` が **デフォルト ON** になった点は、CI/CD と日常開発の挙動に直接影響する。pnpm 自体も pure ESM 化され、Node.js 22+ が必須となった。

## 主な変更点

### サプライチェーン防御がデフォルト ON

- `minimumReleaseAge` のデフォルトが `1440`（1日 = 1440分）
  - npm レジストリに公開されたばかりのバージョンは少なくとも 1 日経過するまでインストールされない
  - 「公開直後にレジストリ汚染で差し替わった悪意あるバージョン」を踏み抜きにくくする
  - opt-out したい場合は `pnpm-workspace.yaml` で `minimumReleaseAge: 0`
- `blockExoticSubdeps` のデフォルトが `true`
  - 推移依存（transitive deps）に Git URL や file: 指定など「異質な」ソースが混入することをブロック
  - 直接 dependencies に書く分には許可される

```yaml
# pnpm-workspace.yaml
minimumReleaseAge: 1440  # 既定値、明示も可
blockExoticSubdeps: true # 既定値
```

### ストア構造を SQLite 1 ファイルに

- 旧: `$STORE/index/` 配下に **数百万の JSON ファイル**
- 新: `$STORE/index.db` という **単一 SQLite データベース**（MessagePack 値、WAL モード）
- 設計理念は「読む量を減らす／システムコールを減らす」
- macOS / Windows のような「小さなファイルが多いと遅い」FS で特にインストール時間が短縮
- バックアップ・同期ツール（Time Machine 等）の負荷軽減にも寄与

### pnpm 自体が pure ESM に

- `.pnpmfile.mjs` に対応（`.cjs` より優先）
- pnpmfile を ESM で書ける → 周辺ツールチェーンと整合
- `require('pnpm')` の内部利用ができなくなったため、pnpm をライブラリとして埋め込んでいた一部ツールは追従が必要

### npm CLI フォールバックを廃止

- 公開コマンド（`pnpm publish`）が npm CLI を呼び出すフォールバックを削除し、ネイティブ実装に統一
- npm CLI の有無に依存しない pipeline が組める

### グローバルインストールの分離

- グローバルパッケージが互いに干渉しないよう、各パッケージごとに分離されたストアを使用
- 古い「グローバル空間で peer dep が衝突する」問題が解消

### Node.js 22+ 必須

- 18 / 19 / 20 / 21 のサポートは廃止

## 破壊的変更・移行ガイド

`pnpm-v10-to-v11` codemod が用意されており、設定の機械的な書き換えはこれで対応できる。

- `package.json` の `pnpm` フィールドはもう読み込まれない
- 設定はすべて **`pnpm-workspace.yaml` に集約**
  - codemod が `package.json` → `pnpm-workspace.yaml` へ移動してくれる
- CI 環境で「直近にリリースされたパッチを即取り込む」運用をしている場合、`minimumReleaseAge` の影響で意図せず古いバージョンが選択されることがある
  - hotfix を当てたい場合は明示的に `--minimum-release-age=0` か `pnpm-workspace.yaml` で 0 を指定
- monorepo で `link:` や Git 依存を多用していた場合、`blockExoticSubdeps` に該当する箇所がないか要確認

## 今後の注目点

- SQLite ストアによる大規模 monorepo での実測スピードアップ（特に CI 上）
- `minimumReleaseAge` 既定 1 日が、エコシステム全体の "公開→即ビルド" 文化をどう変えるか
- Bun / yarn / npm の追従動向（同種のサプライチェーン防御をデフォルト化するか）
- pnpm の Anthropic 経済圏（Bun 買収に続く流れ）への波及はあるか、独立路線を維持するか
