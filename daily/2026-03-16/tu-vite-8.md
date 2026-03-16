# Vite 8.0 — Rolldown 統合による次世代ビルド

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [GitHub Releases](https://github.com/vitejs/vite/releases)

## 概要

Vite 8.0 は、開発時の esbuild と本番用の Rollup という二重バンドラー構成を廃止し、Rust ベースの単一バンドラー **Rolldown** に統一した。Vite 2 以来最大のアーキテクチャ変更であり、ビルド速度は 10〜30 倍の向上が報告されている。

Rolldown は Rollup 互換の API を持ちながら、Rust のパフォーマンスを活かして大規模プロジェクトでも高速なビルドを実現する。既存の Rollup プラグインの多くはそのまま動作する。

## 主な変更点

### Rolldown への統一
- 開発・本番の両方で Rolldown を使用
- Rollup プラグインとの互換レイヤーにより、多くのプロジェクトは変更不要
- 実測値:
  - **Linear**: 46s → 6s
  - **Ramp**: 57% のビルド時間削減
  - **Mercedes-Benz.io**: 最大 38% 削減
  - **Beehiiv**: 64% の削減

### @vitejs/plugin-react v6
- React Refresh の変換に **Oxc** を採用
- Babel 依存を完全削除し、ビルドチェーンがさらに軽量化

### その他の新機能
- 統合 Devtools
- TypeScript path alias のネイティブサポート
- WASM SSR サポート
- lightningcss のバンドル同梱

## 破壊的変更・移行ガイド

### Node.js 要件
- Node.js 20.19+ または 22.12+（Vite 7 と同じ）

### インストールサイズ
- Vite 7 比で約 15MB 増加（lightningcss: 10MB、Rolldown: 5MB）

### 移行手順
1. 多くのプロジェクトはそのままアップグレード可能
2. 複雑な Rollup プラグイン構成を持つプロジェクトは、まず `rolldown-vite` パッケージで段階的に検証することを推奨
3. 公式 [Migration Guide](https://vite.dev/guide/migration) を参照

### Tailwind CSS の対応
- Vite 8.0 リリース当日（3/12）に `@tailwindcss/vite` が Vite 8 対応をマージ
- peer dependency に `^8.0.0` を追加

## 今後の注目点

- **Full Bundle Mode**（実験的）: dev サーバー起動 3 倍高速化、フルリロード 40% 高速化、ネットワークリクエスト 10 分の 1 を目標に開発中
- Rolldown 自体のさらなる最適化と Rollup プラグイン互換性の向上
- エコシステム全体の Vite 8 対応状況（Nuxt, SvelteKit, Astro 等）
