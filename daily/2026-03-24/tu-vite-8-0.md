# Vite 8.0 — Rolldown による統一バンドラーアーキテクチャ

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [Vite Blog](https://vite.dev/blog/announcing-vite8), [Beta 発表](https://vite.dev/blog/announcing-vite8-beta)

## 概要

Vite 8.0 は Vite 2 以来最大のアーキテクチャ変更を含むメジャーリリース。これまで開発時に esbuild、本番ビルドに Rollup という二重バンドラー構成だったものを、Rust 製の統一バンドラー **Rolldown** に一本化した。これにより 10-30x のビルド高速化を実現しつつ、Rollup 互換のプラグイン API を維持している。

## 主な変更点

### Rolldown 統一バンドラー

Vite 8 の中核となる変更。Rolldown は Rust で書かれた高性能バンドラーで、以下の特徴を持つ:

- **10-30x 高速化**: esbuild と同等のパフォーマンスレベルで、Rollup の 10-30 倍高速
- **実績**: Linear の本番ビルドが 46 秒から 6 秒に短縮
- **プラグイン互換性**: Rollup/Vite プラグイン API と互換。ほとんどの既存プラグインがそのまま動作
- **統一バンドラーの利点**: フルバンドルモード、柔軟なチャンク分割、モジュールレベルの永続キャッシュ、Module Federation サポートなど、二重構成では困難だった機能が実現可能に

### Vite DevTools

ビルド分析・デバッグ用の開発者ツールを統合。ビルドプロセスの可視化やボトルネックの特定が容易に。

### tsconfig paths 対応

TypeScript のパスエイリアス（`@/` など）の解析をネイティブサポート。`vite-tsconfig-paths` プラグインが不要に。

### Decorator Metadata 対応

`emitDecoratorMetadata` の自動サポート。NestJS など decorator ベースのフレームワークとの統合が改善。

### Wasm SSR 対応

サーバーサイドレンダリング環境での WebAssembly サポートを追加。

### コンソール転送

ブラウザの console.log 出力を開発サーバーのターミナルに転送する機能を追加。

## 破壊的変更・移行ガイド

### Node.js 要件

**Node.js 20.19 以上または 22.12 以上** が必須。それ以前のバージョンはサポート外。

### インストールサイズの増加

Vite 7 比で約 15MB 増加（lightningcss 約 10MB + Rolldown 約 5MB）。CI/CD のキャッシュ戦略を確認しておくとよい。

### プラグイン互換性

多くのプロジェクトは設定変更なしで動作するが、Rollup 内部 API に依存するプラグインは修正が必要な場合がある。複雑なプロジェクトでは段階的な移行が推奨されている。

### エンドツーエンドツールチェーン

Vite 8 は以下のツールチェーンのエントリポイントとなる:
- **ビルドツール**: Vite
- **バンドラー**: Rolldown
- **コンパイラ**: Oxc

各チームが密に連携し、スタック全体で一貫した動作を保証。

## 今後の注目点

- **Rolldown 単体利用**: Vite を介さずに Rolldown を直接利用するユースケースの拡大
- **Module Federation**: マイクロフロントエンドアーキテクチャとの統合
- **永続キャッシュ**: モジュールレベルのキャッシュによるさらなるビルド高速化
- **エコシステムの対応状況**: 主要プラグイン（Vue、React、Svelte 等）の Vite 8 対応
- **Tailwind CSS v4.2.2**: すでに Vite 8 対応済み
