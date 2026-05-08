# pnpm — v11.0 GA リリース

- **日付**: 2026-04-28（取り上げ日 2026-05-09）
- **カテゴリ**: Build Tool / Package Manager
- **ソース**: [pnpm Blog — 11.0](https://pnpm.io/blog/releases/11.0), [InfoQ — pnpm 11 RC](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/), [Socket — pnpm 11 supply chain protection](https://socket.dev/blog/pnpm-11-adds-new-supply-chain-protection-defaults)

## 概要

pnpm 11 はストアフォーマット・配布形態・既定セキュリティポリシーを刷新したメジャーリリース。最大の変更点はパッケージインデックスの SQLite 化と pnpm 本体の pure ESM 化、そして v10 系で導入された supply-chain 保護のデフォルト ON 化である。Node.js 18 / 19 / 20 / 21 のサポートが落ち、Node.js 22 以上が必須となる。

加えて `pnpm publish` / `login` / `logout` / `view` / `deprecate` / `unpublish` / `dist-tag` / `version` が npm CLI への委譲をやめてネイティブ実装に置き換えられ、グローバルインストールが互いに干渉しないよう完全に分離された。

## 主な変更点

### パッケージインデックスの SQLite 化

- 以前は `$STORE/index/` 配下に何百万もの JSON ファイルを散らしていたが、`$STORE/index.db` 単一の SQLite データベースへ統合。
- 値は MessagePack でエンコード、WAL モードで並行アクセスをサポート。
- バンドルマニフェスト（`name`, `version`, `bin`, `engines`, `scripts` など）をインデックスに直接格納し、解決・インストール時に CAS から `package.json` を読み直す必要をなくした。
- 結果としてストア参照のオーバーヘッドが大幅に削減される。

### pnpm 本体が pure ESM に

- `.pnpmfile.cjs` と並んで `.pnpmfile.mjs` をサポート。
- 両方が存在する場合は `.mjs` が優先され、片方だけがロードされる。
- ESM への移行に伴い、CJS 依存のプラグインや古いツール統合は再確認が必要。

### サプライチェーン保護のデフォルト ON

- `minimumReleaseAge` がデフォルト `1440`（= 1 日）。リリースから 24 時間経過していないバージョンは自動でインストールされない。
- `blockExoticSubdeps` がデフォルト `true`。`git:` / `file:` などレジストリ外ソースを含むサブ依存をブロックする。
- ともに最近続発した npm エコシステムへの supply chain attack を踏まえた既定値。

### npm CLI 依存の解消

- `pnpm publish` などのコマンドが npm CLI を呼び出さず、pnpm 単体で完結するように。
- npm がインストールされていない CI 環境でも publish 系操作が可能になる。

### ランタイム要件の引き上げ

- Node.js 22 以上が必要。Node.js 18, 19, 20, 21 のサポートは削除。

## 破壊的変更・移行ガイド

| 項目 | 影響 | 対応 |
|------|------|------|
| Node.js 18-21 のサポート停止 | pnpm 11 が起動しなくなる | Node.js 22+ にアップグレード |
| `minimumReleaseAge=1440` 既定化 | 公開直後のパッケージが解決失敗する場合がある | CI などで急ぎ必要なら `pnpm install --config.minimumReleaseAge=0` で明示的に上書き |
| `blockExoticSubdeps=true` 既定化 | git 依存などを含むサブ依存があるとエラー | 必要なら `false` に変更、または依存を見直す |
| `.pnpmfile.cjs` と `.pnpmfile.mjs` 両在時の優先度 | 意図せず `.mjs` がロードされる可能性 | どちらか片方に整理する |
| pnpm 本体の ESM 化 | 旧形式プラグインが動かなくなる場合あり | プラグイン側の対応状況を確認 |
| publish 系の npm 委譲廃止 | npm CLI との挙動差で auth 周りが変わる可能性 | `~/.npmrc` の `_auth` / `_authToken` 設定を再確認 |

## 今後の注目点

- SQLite ストアのパフォーマンス効果（特にモノレポでの巨大 lockfile / 大量ワークスペース時）。
- ESM 化に伴うエコシステム側プラグインの追従。
- `minimumReleaseAge` の運用慣習化。今後 npm / yarn 側にも同様の既定化が広がるか注視。
- 公式ブログでは引き続き lockfile / install 周辺の最適化が予告されており、11.x 系のマイナーアップデートでさらに改善が見込まれる。
