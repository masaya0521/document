# Vite 8.0 — Rolldown 統一バンドラーによるアーキテクチャ刷新

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [The Register](https://www.theregister.com/2026/03/16/vite_8_rolldown/)

## 概要

Vite 8.0 は Vite 2 以来最大のアーキテクチャ変更となるリリース。これまで開発時は esbuild、本番ビルドは Rollup という2つのバンドラーを使い分けていたが、Vite 8 では Rust ベースの統一バンドラー **Rolldown** に一本化された。VoidZero チームが開発した Rolldown は、Rollup 互換のプラグイン API を維持しつつ 10-30 倍のビルド高速化を実現する。

## 主な変更点

### Rolldown 統一バンドラー

- **パフォーマンス**: Rollup 比 10-30 倍高速、esbuild と同等のパフォーマンスレベル
- **互換性**: Rollup / Vite と同一のプラグイン API をサポート
- **新機能**: フルバンドルモード、柔軟なチャンク分割、モジュールレベルの永続キャッシュ、Module Federation サポート
- esbuild の `rollupOptions` 設定は互換レイヤーが自動変換

### 実プロジェクトでのベンチマーク

| プロジェクト | ビルド時間改善 |
|---|---|
| Linear | 46秒 → 6秒 |
| Ramp | 57% 短縮 |
| Mercedes-Benz.io | 38% 改善 |
| Beehiiv | 64% 高速化 |

### 新機能

- **統合 DevTools**: `devtools` オプションでデバッグ用開発ツールを有効化
- **TypeScript パスサポート**: `resolve.tsconfigPaths` で tsconfig のパスエイリアス解決が可能に
- **デコレータサポート強化**: TypeScript の `emitDecoratorMetadata` を外部プラグインなしで自動サポート
- **WASM SSR**: `.wasm?init` インポートが SSR 環境で動作
- **コンソール転送**: ブラウザの console.log をサーバーターミナルに転送（AI コーディングエージェントでのエラー検知に有用）
- **@vitejs/plugin-react v6**: Oxc を使用した React Refresh 変換でインストールサイズ削減

### ツールチェーン統合

Vite 8 により、Vite（ビルドツール）/ Rolldown（バンドラー）/ Oxc（コンパイラ）のエンドツーエンドツールチェーンが形成された。

## 破壊的変更・移行ガイド

### 要件

- **Node.js 20.19+ または 22.12+** が必要（Vite 7 と同じ）

### インストールサイズ

Vite 7 比で約 15MB 増加:
- lightningcss（CSS 圧縮の標準依存）: 約 10MB
- Rolldown バイナリ: 約 5MB

### 移行手順

**シンプルなプロジェクト**: そのままアップグレードすれば互換レイヤーが設定を自動変換

**複雑なプロジェクト**: 2段階アプローチを推奨
1. Vite 7 上で `rolldown-vite` パッケージに移行し、バンドラー固有の問題を切り分け
2. その後 Vite 8 にアップグレード

## 今後の注目点

- **フルバンドルモード安定化**: 実験的機能として提供中。開発サーバー起動 3 倍高速化、ネットワークリクエスト 10 分の 1
- **Raw AST 転送**: JavaScript プラグイン向けの生 AST 転送
- **ネイティブ MagicString**: Rust を利用した文字列変換処理
- **Environment API 安定化**: エコシステムとの協調で進行中
