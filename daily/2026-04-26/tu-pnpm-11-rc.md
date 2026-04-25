# pnpm 11 RC — SQLite ストアと供給網セキュリティの強化

- **日付**: 2026-04-21（RC リリース）
- **カテゴリ**: Build Tool / Package Manager
- **ソース**: [InfoQ: pnpm 11 RC](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/), [pnpm Supply Chain Security](https://pnpm.io/supply-chain-security), [pnpm Releases](https://github.com/pnpm/pnpm/releases)

## 概要

pnpm 11 の Release Candidate が 2026-04-21 に公開された。ストアフォーマットの刷新（SQLite 化）、ESM への配布形態切り替え、供給網攻撃対策のデフォルト変更、ビルドスクリプト権限制御の統合など、メジャーバージョンに相応しい踏み込んだ変更が並ぶ。直近数か月で続いた npm エコシステムへの supply chain attack を背景に「セキュリティをデフォルトで強める」方向に大きく舵を切った形。

破壊的変更も多く、Node.js 18–21 のサポートが落ち、Node.js v22 以上が必須となる点、`minimumReleaseAge` がデフォルト 1 日（1440 分）となる点は CI 含めて影響が広いため、アップグレード時の事前検証が必須。

## 主な変更点

### 1. SQLite ベースのストアインデックス

これまでファイルシステム上の構造に依存していたストアインデックスが SQLite に置き換わる。`pnpm install` のメタデータ操作（lookup・整合性確認）が高速化し、巨大モノレポでの体感差が大きいと予想される。ストアフォーマットが変わるため、初回はストアの再構築が走る。

### 2. ESM として配布

pnpm 本体が pure ESM として配布されるようになり、これに伴い **Node.js v22 以上**が必須となった。Node.js 18 / 20 / 21 上では動かなくなる。CI の Node マトリクスや Docker イメージのベースを揃え忘れるとビルドが落ちるので注意。

### 3. supply chain 対策のデフォルト強化

```yaml
# pnpm-workspace.yaml の暗黙的デフォルト
minimumReleaseAge: 1440   # 24 時間（pnpm 11 でデフォルト化）
blockExoticSubdeps: true  # GitHub URL や tarball 直指定の依存をデフォルト拒否
```

`minimumReleaseAge` は pnpm 10.16 で導入された機能で、「公開から指定分数経過していないバージョンは解決対象から除外する」というもの。pnpm 11 ではこれが**デフォルト 1 日**となる。新規に公開された悪性パッケージはコミュニティが概ね 24 時間以内に検知・削除する傾向があるため、デフォルトで 1 日待つだけで多くの zero-day supply chain attack を実効的にブロックできる。

`blockExoticSubdeps` は推移的依存に GitHub URL や tarball URL 指定が入っていた場合にインストールを拒否するセキュリティガード。サプライチェーンを registry 経由に絞ることで監査可能性を高める。

オプトアウトするには `pnpm-workspace.yaml` で `minimumReleaseAge: 0` / `blockExoticSubdeps: false` を明示する。

### 4. ビルドスクリプト設定の統合（`allowBuilds`）

`onlyBuiltDependencies` / `neverBuiltDependencies` / `nodeLinker=isolated` 等に分散していたビルドスクリプト権限の設定が、新しい `allowBuilds` オプションに統合された。

```yaml
allowBuilds:
  - esbuild
  - "@prisma/*"
```

ホワイトリスト方式で「ポストインストールの実行を許可するパッケージ」を明示する設計。デフォルトはホワイトリストに無いものは実行しないという "deny by default" のスタンス。

### 5. グローバルインストールの隔離

`pnpm add -g` で入れた各 CLI が独立したディレクトリ／`node_modules` を持つようになり、グローバル空間での依存衝突が起きなくなる。グローバルパッケージ間で peer dep が壊れる事故を構造的に避けられる。

### 6. 新コマンド

| コマンド | 用途 |
|---------|------|
| `pnpm ci` | ロックファイル厳密モードでのインストール（npm の `npm ci` 相当）。CI 用途で `--frozen-lockfile` を意識せずに済む |
| `pnpm sbom` | プロジェクトの SBOM (Software Bill of Materials) を生成。サプライチェーン監査・コンプライアンス対応に直結 |
| `pnpm clean` | ストア／キャッシュ／node_modules のクリーンアップを統一インターフェースで実行 |

## 破壊的変更・移行ガイド

主な破壊点と対応の指針は以下のとおり。

| 変更 | 影響 | 対応 |
|------|------|------|
| Node.js 18–21 サポート打ち切り | CI / ローカル / Docker で v22 以上が必須 | `nvm` / `volta` / Docker ベースイメージを `node:22` 系に揃える |
| ESM 配布 | スクリプトから pnpm 内部を `require()` していた箇所が壊れる | dynamic `import()` に置換、もしくは CLI 経由で呼び出す |
| `minimumReleaseAge` デフォルト 1440 | 公開直後のバージョンが install で解決されない | パブリッシュ直後にすぐ install 試したい場合は `minimumReleaseAge: 0`、もしくは `--allow-newer` 系のオプトアウトを使用 |
| ストアフォーマット変更 | 初回 install でストア再構築が走る | CI キャッシュの key を pnpm メジャーで分ける |
| ビルドスクリプト設定統合 | `onlyBuiltDependencies` などの旧設定キーは段階的廃止 | `allowBuilds` に書き換え、明示的な許可リスト化 |

ステップとしては「Node 22 化 → pnpm 11 RC で install を試す → ビルドスクリプトで落ちるパッケージを `allowBuilds` に追加 → CI 通過確認」という順が安全。

## 今後の注目点

- RC 期間で得られたフィードバックを踏まえて GA にどの程度デフォルトが残るか（特に `minimumReleaseAge=1440` は議論を呼びやすい設定）
- `pnpm sbom` の SPDX / CycloneDX 互換度合いと、企業の監査ワークフローでの実用性
- `pnpm ci` と従来の `--frozen-lockfile` フラグの将来的な関係（統合か併存か）
- Yarn Berry / Bun の package manager と比較した起動・解決速度の実測ベンチ
