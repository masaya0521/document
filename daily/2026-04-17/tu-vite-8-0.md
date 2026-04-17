# Vite 8.0 — Rolldown 統合によるフルリニューアル

- **日付**: 2026-04-17（元リリース日: 2026-03-12）
- **カテゴリ**: Build Tool
- **ソース**: [Vite 8.0 is out!](https://vite.dev/blog/announcing-vite8), [Vite 8 Beta: The Rolldown-powered Vite](https://vite.dev/blog/announcing-vite8-beta), [Vite Migration Guide](https://main.vite.dev/guide/migration)

## 概要

Vite 8.0 は Vite 2 以来最大規模のアーキテクチャ変更となるメジャーリリース。従来 dev には esbuild、本番ビルドには Rollup という二重構成だったが、8.0 からは Rust 実装のバンドラー **Rolldown** に統一された。Linear が 46 秒 → 6 秒、Mercedes-Benz.io が最大 38% 短縮など、実プロジェクトでのビルド時間改善事例が具体的に報告されている。

## 主な変更点

### Rolldown の統合

- dev/prod ともに Rolldown を採用し、`esbuild` ベースの dep optimization、`rollup` ベースの本番ビルドという二重実装が解消。
- プラグイン API は Rollup 互換を維持（既存 Rollup プラグインの多くがそのまま動作）。
- `build.rollupOptions` と `optimizeDeps` の設定は内部で Rolldown 用に自動変換される互換レイヤーが提供される。

### パフォーマンス

- 公式の発表では **10〜30 倍の本番ビルド高速化**。
- 公表されている導入事例:
  - Linear: 46s → 6s
  - Beehiiv: 64% 削減
  - Mercedes-Benz.io: 最大 38% 削減

### 依存関係とサイズ

- `lightningcss` が optional から通常の依存に変更（~10 MB 増）。
- Rolldown 本体が ~5 MB。
- 合計でインストールサイズが Vite 7 比 **約 15 MB 増**。

## 破壊的変更・移行ガイド

### 必要な環境

- **Node.js 20.19+ または 22.12+** が必須。
- ESM-only の配布に切り替わったため、CJS から動的 `require('vite')` していた箇所は `import()` へ書き換えが必要。

### 設定の移行

ほとんどのプロジェクトは設定変更なしで 8.0 にアップグレードできるが、以下を確認する:

1. `build.rollupOptions.plugins` / `optimizeDeps.esbuildOptions` などが Rolldown プラグイン API にマップできるか。
2. Rollup プラグインの一部は Rolldown での動作が未検証。公式 Migration Guide の互換テーブルを参照。
3. Node 版要件を満たすか（20.19 / 22.12 がライン）。
4. CSS 系で `lightningcss` がデフォルト処理されるため、既存の PostCSS/autoprefixer の挙動を再確認。

### 推奨アップグレード手順

```bash
# 1. バージョンアップ
npm install vite@^8 --save-dev

# 2. 開発サーバーで警告・差異を確認
npm run dev

# 3. 本番ビルドで出力サイズ・時間を比較
npm run build

# 4. プラグインのアップデート
# vite-plugin-* の多くが Vite 8 対応のバージョンをリリース済み
```

## 今後の注目点

- **Rolldown 単体の GA**: Vite 8 のベータ期間中に Rolldown 本体も beta → RC へ進捗。単体利用（Rollup 代替として）のエコシステム整備が進む見通し。
- **OXC との連携**: Rust 製 JS/TS ツールチェーン「Oxc」との統合が進むと、lint/format/bundle が Rust 製に収束する流れ。Biome との棲み分けが今後の論点。
- **Vite 7 の LTS 的位置づけ**: 7.3 系に重要な修正・セキュリティパッチがバックポートされる。移行に時間がかかるプロジェクトは 7.3 で待機する選択肢もある。
- **Next.js との差別化**: Turbopack（Next.js 16.2 で更に高速化）と Rolldown がそれぞれ独自のエコシステムを形成しており、bundler 選定基準が「フレームワーク純正 vs 汎用 Rust バンドラー」に整理されていく。
