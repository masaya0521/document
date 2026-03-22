# Vite 8.0 — Rolldown 統合による統一バンドラー時代の到来

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [The Register](https://www.theregister.com/2026/03/16/vite_8_rolldown/)

## 概要

Vite 8.0 は、開発用の esbuild と本番用の Rollup という 2 つのバンドラーを、Rust 製の統一バンドラー **Rolldown** に置き換えた歴史的なリリース。Vite 2 以来最大のアーキテクチャ変更であり、ビルド速度 10-30 倍の高速化を実現しつつ、既存の Rollup/Vite プラグイン互換性を維持している。

## 主な変更点

### Rolldown 統合
- 開発・本番ビルドの両方で単一の Rust 製バンドラーを使用
- Rollup と同じプラグイン API をサポートし、既存プラグインの大半がそのまま動作
- 10-30 倍のビルド高速化（esbuild と同等のパフォーマンスレベル）

### 統一バンドラーで可能になった新機能
- **フルバンドルモード**: 開発時にもバンドルされた出力が可能に
- **柔軟なチャンク分割**: より細かいバンドル最適化
- **モジュールレベルの永続キャッシュ**: 増分ビルドのさらなる高速化
- **Module Federation サポート**: マイクロフロントエンド対応

### その他の新機能
- **Vite DevTools**: ビルド解析・デバッグ用の統合ツール
- **TypeScript tsconfig パスのネイティブサポート**: `resolve.alias` 不要に
- **`emitDecoratorMetadata` の自動サポート**
- **Wasm SSR 環境対応**: WebAssembly をサーバーサイドで利用可能
- **ブラウザコンソールのターミナル転送**: ブラウザの console.log がターミナルに表示
- **プラグインレジストリ**: registry.vite.dev で Vite/Rolldown/Rollup プラグインを検索可能

## 破壊的変更・移行ガイド

- **Node.js 20.19 以上が必須**（Vite 7 と同じ要件）
- **インストールサイズが約 15MB 増加**（Rolldown バイナリの追加による）
- esbuild / Rollup に直接依存するカスタムプラグインは修正が必要な場合あり
- 詳細は[マイグレーションガイド](https://vite.dev/guide/migration)を参照

## 今後の注目点

- Rolldown 自体の継続的な最適化（さらなるビルド速度向上）
- Turbopack との競争・差別化の行方
- Vite DevTools のエコシステム拡大
- Module Federation を活用したマイクロフロントエンドの実践事例
