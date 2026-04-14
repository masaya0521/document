# Vite 8.0 — Rolldown 統合による次世代ビルドツールチェーン

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [Beta 発表](https://vite.dev/blog/announcing-vite8-beta)

## 概要

Vite 8.0 は Vite 2 以来最大のアーキテクチャ変更を含むメジャーリリース。これまで開発時に esbuild、本番ビルドに Rollup という二重パイプラインだった構成を、Rust ベースの統一バンドラー **Rolldown** に一本化した。VoidZero チームが開発した Rolldown は、Rollup 互換のプラグイン API を維持しつつ、ネイティブ速度で動作する。

Vite は本リリースにより、ビルドツール（Vite）・バンドラー（Rolldown）・コンパイラ（Oxc）が密に連携するエンドツーエンドのツールチェーンとなった。

## 主な変更点

### Rolldown バンドラーへの統一

- esbuild と Rollup を Rolldown に置き換え
- Rollup と同じプラグイン API をサポート（既存プラグインの大半がそのまま動作）
- 互換性レイヤーにより、既存の `esbuild` / `rollupOptions` 設定を自動変換

### パフォーマンス改善

実プロジェクトでの計測結果:

| プロジェクト | 改善率 | 詳細 |
|---|---|---|
| Linear | **87% 削減** | 46秒 → 6秒 |
| Beehiiv | **64% 削減** | — |
| Ramp | **57% 削減** | — |
| Mercedes-Benz.io | **38% 削減** | — |

公称値として **10-30 倍** の高速化を謳っている。

### 新機能

- **フルバンドルモード**: 開発時もバンドルを行い、本番環境との挙動差を削減
- **モジュールレベル永続キャッシュ**: インクリメンタルビルドの高速化
- **柔軟なチャンク分割**: より細かいコード分割制御
- **Vite Plugin Registry**: [registry.vite.dev](https://registry.vite.dev) — Vite / Rolldown / Rollup プラグインの検索可能なディレクトリ
- **統合 DevTools**: Vite Inspector がビルトインで利用可能

## 破壊的変更・移行ガイド

### 必須要件

- **Node.js 20.19+ または 22.12+** が必要（Node.js 18 はサポート終了）
- インストールサイズが約 **15MB 増加**（lightningcss: ~10MB, Rolldown: ~5MB）

### 移行手順

1. `vite` パッケージを v8 に更新
2. 多くのプロジェクトでは設定変更なしで動作（互換性レイヤーが自動変換）
3. カスタム `rollupOptions` を使用している場合は、Rolldown の対応状況を確認
4. esbuild 固有の設定（`esbuild.transform` 等）を使用している場合は Oxc の同等オプションに移行

複雑なプラグイン構成を持つプロジェクトでは段階的な移行が推奨される。

## 今後の注目点

- Rolldown 自体の安定化と残りの Rollup プラグイン互換性の向上
- Oxc コンパイラとの統合深化（transformer, minifier, linter）
- フルバンドルモードのパフォーマンスチューニング
- Vite 8 を基盤とした Next.js / Nuxt / Astro 等のフレームワーク対応状況
- React Router v7.14.0 が早速 Vite 8 対応を完了しており、エコシステムの移行が加速中
