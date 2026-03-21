# Vite 8.0 — Rolldown 統合による次世代ビルドツール

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8)

## 概要

Vite 8.0 は Rolldown を単一の統合バンドラーとして採用した最も重要なアーキテクチャ変更リリース。これまで開発時は esbuild、本番ビルドは Rollup という二重構成だったものを、Rust ベースの Rolldown に一本化し、10-30x の高速ビルドを実現した。既存の Vite/Rollup プラグインとの互換性を維持しつつ、フルバンドルモードやモジュールレベルの永続キャッシングなどの高度な機能も可能にしている。

## 主な変更点

### Rolldown 統合
- Rust 製の統合バンドラーで開発・本番の両方を処理
- Rollup と同一のプラグイン API をサポートし、既存プラグインはそのまま動作
- esbuild レベルのパフォーマンスと Rollup レベルの柔軟性を両立

### 実運用でのパフォーマンス実績
- **Linear**: 46秒 → 6秒（87% 削減）
- **Ramp**: 57% 削減
- **Mercedes-Benz.io**: 最大 38% 削減
- **Beehiiv**: 64% 削減

### 新機能
- **Vite DevTools** の統合
- **TypeScript パスエイリアス** の自動解決
- **emitDecoratorMetadata** サポート
- **WebAssembly の SSR 対応**
- **ブラウザコンソール転送**: ブラウザのコンソール出力をターミナルに転送
- より柔軟なチャンク分割戦略
- Module Federation サポート

### 今後の実験的機能
- **フルバンドルモード**: 開発時のバンドル化で 3x 高速なサーバー起動を予測
- **Raw AST 転送**: JS プラグインから Rust 生成 AST へのアクセス
- **ネイティブ MagicString**: カスタム変換の最適化
- **Environment API** の安定化

## 破壊的変更・移行ガイド

### 要件
- Node.js 20.19+ または 22.12+ が必須（Vite 7 と同じ）
- インストールサイズが約 15MB 増加（lightningcss 約 10MB + Rolldown 約 5MB）

### 推奨マイグレーション手順
1. 複雑なプロジェクトでは、まず Vite 7 で `rolldown-vite` パッケージに切り替えて動作確認
2. その後 Vite 8 にアップグレード
3. 既存の設定は自動変換レイヤーにより大部分が互換

### エコシステムの対応状況
- Tailwind CSS v4.2.2 が Vite 8 対応済み
- SvelteKit 2.53.0 が Vite 8 サポート開始

## 今後の注目点

- フルバンドルモードの安定化時期（開発時バンドルの実用性）
- Rolldown の Rollup プラグイン互換性のカバレッジ向上
- Environment API の安定版リリース
- Vite 8 対応のエコシステム拡大（各種フレームワーク・ツールの対応状況）
