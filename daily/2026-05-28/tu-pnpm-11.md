# pnpm 11 — SQLite ストア・サプライチェーン保護・pacquet 統合

- **日付**: 2026-05-28
- **カテゴリ**: Build Tool / パッケージマネージャ
- **ソース**: [pnpm 11.0 リリース](https://pnpm.io/blog/releases/11.0), [pnpm 11.2 リリース](https://pnpm.io/blog/releases/11.2), [GitHub Releases](https://github.com/pnpm/pnpm/releases)

## 概要

pnpm 11.0 が 2026年4月28日にリリースされ、アーキテクチャとセキュリティモデルの両面で大きな転換を迎えた。ストアインデックスを JSON ファイルから SQLite に移行し、サプライチェーン保護をデフォルトで有効化。さらに 11.2（5月20日）では、Rust で書き直された pacquet をインストールバックエンドとして実験的に統合し、パフォーマンス面でも新しい方向性を示している。

## 主な変更点

### アーキテクチャ変更

- **SQLite ストアインデックス**: パッケージごとの JSON ファイルを単一の SQLite データベースに置き換え。ファイルシステムの負荷軽減と検索パフォーマンス向上
- **グローバルインストールの隔離**: 各グローバルパッケージが独立ディレクトリで隔離され、パッケージ間の干渉を排除
- **ネイティブ publish 実装**: npm CLI へのフォールバックを廃止し、pnpm 独自の publish フローに完全移行
- **ESM 専用**: pnpm 自体が Pure ESM に移行

### セキュリティ強化

- **`minimumReleaseAge`**: デフォルト値が `1440`（1日）に設定。npm レジストリに公開された直後のパッケージのインストールをブロック
- **`blockExoticSubdeps`**: デフォルト有効。サブ依存関係が Git URL や tarball など非標準ソースを参照している場合にブロック
- **GHSA ベースの監査**: CVE ID から GHSA ID ベースのフィルタリングに移行

### 新コマンド

- `pnpm clean` — node_modules の削除
- `pnpm sbom` — SPDX / CycloneDX 形式のソフトウェア部品表（SBOM）生成
- `pnpm with` — 特定バージョンの pnpm でコマンド実行
- `pnpm audit signatures`（11.1）— パッケージ署名の検証
- `pnpm bugs`, `pnpm owner`（11.1）— npm 互換コマンド追加

### pacquet 統合（11.2、実験的）

pnpm 11.2 で、Rust で実装された pacquet をインストールバックエンドとして利用可能になった。

```yaml
# pnpm-workspace.yaml の configDependencies に追加
# pnpm add @pnpm/pacquet --config
```

- pnpm が依存関係の解決（resolution）を担当し、pacquet はフェッチとインポート（materialization）のみを担当
- lockfile 生成後の処理を Rust で高速化するアプローチ
- 現時点では実験的オプトイン

## 破壊的変更・移行ガイド

### 環境要件

| 項目 | pnpm 10 | pnpm 11 |
|------|---------|---------|
| Node.js | 18+ | 22+ |
| モジュール形式 | CJS/ESM | ESM 専用 |
| glibc（スタンドアロン） | 2.17+ | 2.27+ |

### 設定の移行

pnpm 固有の設定は `.npmrc` から `pnpm-workspace.yaml` または新グローバル `config.yaml` に移行が必要。`.npmrc` は認証・レジストリ設定のみの役割に限定された。

```yaml
# 旧: .npmrc
# shamefully-hoist=true
# strict-peer-dependencies=false

# 新: pnpm-workspace.yaml
packages:
  - "packages/*"
shamefullyHoist: true
strictPeerDependencies: false
```

環境変数プレフィックスも `npm_config_*` から `pnpm_config_*` に変更。

### ビルド設定

複数あったビルド関連オプション（`onlyBuiltDependencies`, `neverBuiltDependencies` 等）が `allowBuilds` マップに統一。

### 監査設定

```yaml
# 旧
pnpm:
  auditConfig:
    ignoreCves:
      - CVE-2023-XXXXX

# 新
pnpm:
  auditConfig:
    ignoreGhsas:
      - GHSA-xxxx-xxxx-xxxx
```

### 推奨移行手順

1. Node.js 22 以上にアップグレード
2. `.npmrc` の pnpm 固有設定を `pnpm-workspace.yaml` に移行
3. ビルド設定を `allowBuilds` に統一
4. CVE フィルタを GHSA フィルタに更新
5. `pnpm setup` を再実行（グローバルインストールの PATH 更新）
6. 公式 [マイグレーションガイド](https://pnpm.io/migration) のコードモッド活用を推奨

## 今後の注目点

- pacquet の安定化とパフォーマンスベンチマーク公開
- SBOM 生成の CI/CD パイプラインへの統合事例
- Bun のパッケージマネージャとのパフォーマンス競争の行方
- サプライチェーン保護のデフォルト有効化が他のパッケージマネージャに与える影響
