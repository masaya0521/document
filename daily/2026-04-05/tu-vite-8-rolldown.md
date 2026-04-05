# Vite 8.0 — Rolldown 統合で JavaScript ビルドツールの新時代へ

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [GitHub Releases](https://github.com/vitejs/vite/releases)

## 概要

Vite 8.0 は、開発環境用の esbuild と本番環境用の Rollup という二重バンドラー構成を廃止し、Rust 製の統合バンドラー **Rolldown** に一本化した。これは Vite 2 以来最大のアーキテクチャ変更であり、ビルド速度は 10-30x の高速化を実現している。Rolldown は VoidZero チーム（Vue.js / Vite 作者の Evan You が 2024 年末に設立）が開発し、2026 年 1 月に 1.0 RC に到達した。

## 主な変更点

### Rolldown 統合（最大の目玉）

- esbuild（開発時の依存関係事前バンドル）と Rollup（本番ビルド）を Rolldown に統一
- Rollup 互換 API を維持し、既存プラグインエコシステムがそのまま動作
- 統一バンドラーにより、フルバンドルモード、柔軟なチャンク分割、モジュールレベルの永続キャッシュ、Module Federation が可能に

**実際の企業での改善実績:**

| 企業 | 改善幅 | 詳細 |
|------|--------|------|
| Linear | 46s → 6s | 約 87% 削減 |
| Ramp | 57% 短縮 | — |
| Mercedes-Benz.io | 最大 38% 削減 | — |
| Beehiiv | 64% 短縮 | — |

### Vite Devtools 統合

`devtools` オプションでビルトインのデバッグ・分析ツールを有効化可能。

### TypeScript パス別名サポート

`resolve.tsconfigPaths` を有効にすることで、`tsconfig.json` のパスマッピングを自動解決。

### Wasm SSR 対応

`.wasm?init` インポートが SSR 環境で動作するようになり、WebAssembly を使ったサーバーサイドレンダリングが可能に。

### ブラウザコンソール転送

`server.forwardConsole` により、ブラウザ側の `console.log` やエラーを dev サーバーのターミナルに転送。コーディングエージェント検出時は自動有効化される。

### @vitejs/plugin-react v6

React Refresh の変換に Oxc を使用し、Babel への依存を完全に除去。インストールサイズが大幅に削減。

## 破壊的変更・移行ガイド

### 動作要件

- **Node.js 20.19+ / 22.12+** が必須（Node.js 18 サポート終了）

### バンドラー移行

- 既存の `esbuildOptions` および `rollupOptions` は互換レイヤーで自動変換される
- ただし、Rolldown 固有の設定に移行することを推奨
- Rolldown のミニフィケーション機能はまだアルファ段階

### インストールサイズ

- Vite 7 比で約 15MB 増加（lightningcss 約 10MB + Rolldown 約 5MB）
- バンドラーを 2 つ持つ必要がなくなったため、トータルの依存関係は簡素化

## 今後の注目点

- **フルバンドルモード**: 開発時も本番と同じバンドルを使う実験的機能
- **Raw AST 転送**: プラグイン間で AST を直接渡し、パース/シリアライズのオーバーヘッドを削減
- **ネイティブ MagicString 変換**: ソースマップ生成の高速化
- **Rolldown 1.0 正式リリース**: 現在はまだ RC 段階。ミニフィケーションのアルファ卒業が鍵
- **registry.vite.dev**: Vite / Rolldown / Rollup プラグインの検索可能なディレクトリが新設（npm から毎日データ収集）
