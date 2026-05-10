# pnpm 11 — サプライチェーン防御を既定化、SQLite ストアと ESM 化

- **日付**: 2026-05-10
- **カテゴリ**: Build Tool / Package Manager
- **ソース**: [pnpm 11.0 リリースノート](https://pnpm.io/blog/releases/11.0), [InfoQ の解説](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/), [cybersecuritynews](https://cybersecuritynews.com/pnpm-11-turns-on-minimum-release-age/)

## 概要

pnpm v11.0 が 2026-04-28 にリリース。v10 の系統で導入された各種サプライチェーン保護を**デフォルトで有効化**する点が最大のトピック。あわせて、内部ストアの実装を JSON-per-package から単一 SQLite データベースへ刷新、CLI 自体を ESM 化、Node.js 22 以上を必須にするなど、メジャーリリースに相応しい大きな書き換えが入っている。

5 月時点ですでに `pnpm` の週次 DL は 7,000 万を超えており、CI / 開発機の更新計画は 1〜2 ヶ月以内に立てるのが現実的。

## 主な変更点

### サプライチェーン保護のデフォルト強化

`v10` で opt-in だった以下の設定が `v11` でデフォルトオン:

- `minimumReleaseAge = 1440` (= 24 時間): 公開直後 1 日以内のバージョンは自動でインストール対象から除外。npm レジストリ経由の急性的サプライチェーン攻撃（公開 → 数時間以内に被害拡大）への有効な防御
- `blockExoticSubdeps = true`: tarball URL / git URL / file: 等、レジストリ以外から導入される推移的依存をブロック
- 新しい "Allow Builds" モデル: install 中にビルドスクリプトを実行できるパッケージをユーザーが明示的に許可リスト管理する仕組み

### 内部ストアを SQLite 化

- これまでは依存パッケージごとに JSON ファイルを持つ構造だったため、巨大 monorepo で I/O が膨らむ問題があった
- v11 ではストアインデックスを単一の SQLite DB に統合し、I/O 効率と整合性を改善

### ESM 化と publish の刷新

- pnpm CLI 本体が pure ESM へ移行
- これまで内部的に npm CLI にフォールバックしていた `pnpm publish` を、native 実装で完全置き換え
- グローバルインストールが互いに干渉しないよう分離

### 依存環境の要件変更

- **Node.js 22 以上が必須**。Node 18 / 19 / 20 / 21 のサポートを drop
- スタンドアロン実行ファイルは glibc 2.27 以上を要求

## 破壊的変更・移行ガイド

### 主な破壊的変更

- Node.js 22 未満では起動しない（CI / Docker base image / dev container を要更新）
- サプライチェーン保護のデフォルトが厳しくなったため、新規依存追加時に「24 時間待たないと入らない」挙動に変わる
- exotic subdep を多用するプロジェクトでは install が落ちる可能性あり

### 公式 codemod

ほとんどの設定変更は機械的に行えるため、公式の codemod が用意されている:

```bash
npx pnpm-v10-to-v11
```

`.npmrc` / `pnpm-workspace.yaml` の設定キーを v11 仕様へ自動変換する。

### 移行時のチェックリスト

1. CI で利用する Node.js を 22 以上に揃える
2. Docker base image / GitHub Actions の `setup-node` バージョン更新
3. プライベートレジストリ / Verdaccio 等を使っている場合、`minimumReleaseAge` で社内パッケージの公開反映が遅れる可能性 → `minimumReleaseAge` を社内スコープのみ短縮するか、社内パッケージ用に override 設定
4. `pnpm publish` が変わったため、CI の publish ジョブを最新挙動で動作確認
5. 依存パッケージで build scripts を持つもの（`node-gyp` 系、Sharp、Prisma 等）は Allow Builds 設定が必要

## 今後の注目点

- npm 系列のサプライチェーン攻撃（typosquatting、メンテナアカウント乗っ取り、ポストインストールバックドア）に対する**業界標準のデフォルト**を pnpm が先導した形。Yarn / npm 本体の追従が起こるかが今後の見どころ
- SQLite ストアによりパフォーマンスは向上するが、ストア破損時の復旧手順や、複数ユーザー共有 store でのロック挙動は注意点。大規模 monorepo は早めに自社環境で計測しておくのが安全
- ESM 化と Node.js 22+ 要件は、古い CLI ラッパーや OS パッケージ（Debian / Ubuntu LTS のシステム Node）と競合する可能性が高い。社内の bootstrap スクリプトを総点検する好機
