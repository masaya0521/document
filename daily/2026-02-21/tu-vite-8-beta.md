# Vite 8.0 Beta — Rolldown 統合による次世代ビルド

- **日付**: 2025-12-03（初回 Beta）/ 2026-02-19（beta.15）
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8-beta), [VoidZero](https://voidzero.dev/posts/announcing-vite-8-beta), [GitHub Releases](https://github.com/vitejs/vite/releases)

## 概要

Vite 8 は、従来の esbuild（開発時）+ Rollup（本番ビルド）という二重バンドラー構成を廃止し、**Rolldown**（Rust 製の統合バンドラー）に一本化する。これにより開発・本番環境間の不整合を解消しつつ、本番ビルドを 10-30 倍高速化する。

Rolldown は VoidZero（Evan You 率いるチーム）が開発しており、Vite + Rolldown + Oxc による end-to-end の Rust ベースツールチェーンが実現する。既存の Rollup/Vite プラグインの大部分はそのまま動作する。

## 主な変更点

### Rolldown 統合

- **二重バンドラーの廃止**: 開発時（esbuild）と本番（Rollup）の分離を解消し、単一の変換パイプラインに統一
- **Rollup 互換プラグイン API**: 既存の Rollup/Vite プラグインの大部分がそのまま動作
- **グルーコードの削減**: esbuild と Rollup の差異を吸収するための内部コードが不要に

### パフォーマンス改善

| 指標 | 改善内容 |
|------|---------|
| 本番ビルド速度 | Rollup 比 10-30x 高速 |
| Linear 社 | 46 秒 → 6 秒 |
| Ramp 社 | 57% 削減 |
| Full Bundle Mode（実験的） | 大規模プロジェクトで 3x 高速なサーバー起動 |

### 新機能

- **tsconfig paths 対応**: `resolve.tsconfigPaths` オプションで tsconfig.json のパスマッピングをネイティブサポート
- **emitDecoratorMetadata 自動対応**: TypeScript のデコレータメタデータ出力を組み込みでサポート
- **ブラウザターゲットの整理**: Baseline Widely Available に合わせたターゲット設定

### Full Bundle Mode（実験的）

開発サーバーでも本番と同様にバンドルを行うモード。大規模プロジェクトにおけるモジュール数の爆発を抑え、サーバー起動を 3 倍高速化する。現在は実験段階。

## 破壊的変更・移行ガイド

### 設定の変更

Rollup や esbuild 固有のオプションに依存している場合は設定調整が必要：

- `build.rollupOptions` の一部オプションが Rolldown では異なる挙動を示す可能性
- esbuild 固有の設定（`esbuild` オプション）は Rolldown/Oxc ベースの設定に移行

### 移行ステップ

1. Vite 8 Beta をインストール:
   ```bash
   npm install vite@beta
   ```
2. フレームワーク（Next.js, Nuxt 等）を使用している場合は `package.json` でオーバーライド:
   ```json
   {
     "overrides": {
       "vite": "^8.0.0-beta.0"
     }
   }
   ```
3. [移行ガイド](https://main.vite.dev/guide/migration) に従い、Rollup/esbuild 固有の設定を確認・調整
4. プラグインの互換性をテスト（大部分はそのまま動作）

## 今後の注目点

- **安定版リリース**: Beta が活発に更新中（beta.15 まで到達）。安定版は 2026 年前半の見込み
- **Full Bundle Mode の安定化**: 大規模プロジェクトでの開発体験を大幅に改善する可能性
- **Rolldown の独立利用**: Vite 以外のプロジェクトでも Rolldown を直接バンドラーとして利用可能
- **Module Federation サポート**: マイクロフロントエンド構成の組み込みサポート
- **モジュールレベル永続キャッシュ**: 再ビルド時のさらなる高速化
