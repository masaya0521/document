# Vite 8.0 — Rolldown 統合による 10-30x 高速化

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [Vite Blog](https://vite.dev/blog/announcing-vite8), [The Register](https://www.theregister.com/2026/03/16/vite_8_rolldown/)

## 概要

Vite 8.0 は、Rust 製バンドラー Rolldown を単一の統合バンドラーとして採用した歴史的なリリースである。従来の「開発時は esbuild、本番は Rollup」という二重構造を解消し、Rolldown 一本に統一することで 10-30x のビルド高速化を実現した。Vite 2 以来最大のアーキテクチャ変更であり、開発・本番間の挙動差異の解消や、Module Federation・永続キャッシュなど従来不可能だった機能を可能にしている。

## 主な変更点

### Rolldown 統合

Rolldown は Rollup 互換の API を持つ Rust 製バンドラーで、esbuild 並みの速度と Rollup の最適化能力を兼ね備える。主な利点:

- **単一バンドラー**: 開発・本番で同じバンドラーを使用し、環境差異を解消
- **フルバンドルモード**: 開発時もバンドルが可能に
- **柔軟なチャンク分割**: より細かい制御が可能
- **モジュールレベル永続キャッシュ**: 再ビルドの高速化
- **Module Federation サポート**: マイクロフロントエンド対応

### 実例ベンチマーク

| 企業 | 改善 | 詳細 |
|---|---|---|
| Linear | 87% 削減 | 46 秒 → 6 秒 |
| Ramp | 57% 削減 | — |
| Mercedes-Benz.io | 最大 38% 削減 | — |
| Beehiiv | 64% 削減 | — |

### 新機能

- **統合 DevTools**: `devtools` オプションでビルド分析・デバッグツールを組み込み
- **Wasm SSR**: WebAssembly の SSR 環境サポート
- **TypeScript パスエイリアス**: `resolve.tsconfigPaths` でネイティブ対応
- **`emitDecoratorMetadata` 自動対応**: 外部プラグイン不要に
- **ブラウザコンソールログ転送**: ブラウザの console.log を dev サーバーターミナルに表示
- **プラグインレジストリ**: registry.vite.dev で Vite / Rolldown / Rollup プラグインを検索可能

### プラグイン互換性

Rolldown は Rollup と同一のプラグイン API をサポートするため、既存の Vite プラグインの大部分がそのまま動作する。互換レイヤーにより、`esbuild` や `rollupOptions` の設定は自動的に Rolldown 相当に変換される。

## 破壊的変更・移行ガイド

### インストールサイズ

Vite 7 比で約 15MB 増加（lightningcss 10MB + Rolldown 5MB）。ただしビルド速度の改善で十分に相殺される。

### 設定の自動変換

```js
// vite.config.js — 多くの場合変更不要
export default defineConfig({
  // esbuild や rollupOptions の設定は
  // 互換レイヤーが Rolldown に自動変換
})
```

明示的に Rolldown 固有の設定を使いたい場合は `rolldownOptions` を使用する。

### エコシステム対応

Tailwind CSS は Vite 8 リリース当日に `@tailwindcss/vite` の peer dependency を `^8.0.0` に拡張済み。

## 今後の注目点

- **Rolldown 単体利用**: Vite 外でも Rolldown を直接使うユースケースの拡大
- **永続キャッシュの成熟**: モジュールレベルキャッシュの最適化と安定化
- **Vite エコシステム**: プラグインの Rolldown ネイティブ対応への移行
- **他ツールへの影響**: Turbopack や webpack との競争激化
