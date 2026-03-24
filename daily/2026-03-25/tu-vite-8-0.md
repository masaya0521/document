# Vite 8.0 — Rolldown 統合による Rust ベースビルドツールチェーンへの転換

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [GitHub Releases](https://github.com/vitejs/vite/releases)

## 概要

Vite 8.0 は、開発用の esbuild と本番用の Rollup という二重構成を廃止し、Rust 製の統一バンドラー Rolldown を統合した。Vite 2 以来最大のアーキテクチャ変更であり、ビルド速度は最大 10-30x 高速化される。Vite はバンドラー（Rolldown）とコンパイラ（Oxc）と密接に連携するエンドツーエンドのツールチェーンへと進化した。

## 主な変更点

### Rolldown 統合

Rolldown は Rust で書かれた JavaScript バンドラーで、Rollup との API 互換性を保ちつつネイティブレベルのパフォーマンスを実現する。これにより開発と本番で同一のバンドラーが使用され、環境間の挙動差が解消される。

### パフォーマンス改善の実績

実プロダクションでの改善報告:

| 企業 | 改善内容 |
|------|---------|
| Linear | 46秒 → 6秒 |
| Beehiiv | ビルド時間 64% 削減 |
| Mercedes-Benz.io | 最大 38% 削減 |

### 新機能

- **Vite Devtools 統合**: 開発時のデバッグ機能を強化
- **TypeScript パス別名の自動解決**: `resolve.tsconfigPaths: true` で設定可能
- **Oxc ベースの React Plugin v6**: Babel 依存が削除され、インストールサイズが縮小
- **WebAssembly SSR 対応**: サーバーサイドレンダリングでの Wasm 利用が拡張
- **ブラウザコンソール転送**: ブラウザのログをターミナルに直接出力
- **プラグインレジストリ**: registry.vite.dev で Vite/Rolldown/Rollup プラグインを検索可能
- **emitDecoratorMetadata 自動サポート**: TypeScript のデコレータメタデータを自動処理

### システム要件

- Node.js 20.19 以上、または 22.12 以上が必須

### インストールサイズ

前バージョンより約 15MB 増加:
- lightningcss 統合: 約 10MB
- Rolldown バイナリ: 約 5MB

## 破壊的変更・移行ガイド

- esbuild から Rolldown への切り替えにより、一部のプラグインが互換性の調整を必要とする可能性がある
- Rollup プラグインの大部分はそのまま動作するが、Rollup 固有の内部 API に依存するプラグインは更新が必要
- Node.js の最小バージョンが引き上げられた

## 今後の注目点

- **Rolldown の成熟**: 統合初期リリースのため、エッジケースでの互換性改善が継続される見込み
- **Oxc エコシステム**: Oxc（Rust ベース JS コンパイラ）との連携がさらに深化し、トランスパイル・最適化の両面で高速化が期待される
- **エコシステム対応**: Astro 6.0 が既に Vite 8 を採用。主要フレームワーク（Next.js、Nuxt、SvelteKit 等）の対応状況に注目
