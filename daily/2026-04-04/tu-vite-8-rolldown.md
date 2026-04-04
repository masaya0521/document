# Vite 8 — Rolldown 統合によるアーキテクチャ刷新

- **日付**: 2026-03-12（正式リリース）
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [Beta 発表](https://vite.dev/blog/announcing-vite8-beta), [The Register](https://www.theregister.com/2026/03/16/vite_8_rolldown/)

## 概要

Vite 8 は、Vite 2 以来最大のアーキテクチャ変更となるリリース。従来の esbuild（開発時）+ Rollup（本番ビルド）という二重バンドラー構成を廃止し、Rust ベースの統一バンドラー **Rolldown** に一本化した。これにより開発・本番環境間の挙動差異が解消され、ビルド速度は 10〜30倍向上した。

週間ダウンロード数は 6,500万回を超え、フロントエンドエコシステムの中核ツールとしての地位を確固たるものにしている。

## 主な変更点

### Rolldown 統合

- **単一バンドラー**: esbuild と Rollup の役割を Rolldown が統合。開発と本番で同一のバンドラーが動作するため、環境差異によるバグが大幅に減少
- **Rollup 互換プラグイン API**: 既存の Rollup プラグインの大半がそのまま動作する互換性レイヤーを提供
- **段階的移行**: Vite 7 時代に `rolldown-vite` パッケージとしてテクニカルプレビューを提供し、コミュニティ主導で互換性検証を実施

### パフォーマンス改善（実測値）

| プロジェクト | 改善 |
|---|---|
| Linear | 46秒 → 6秒（87%削減） |
| Ramp | 57%削減 |
| Mercedes-Benz.io | 38%削減 |
| Beehiiv | 64%削減 |

### Full Bundle Mode（実験的）

- 開発サーバー起動: 3倍高速
- フルリロード: 40%高速
- ネットワークリクエスト数: 10分の1

### その他の新機能

- **Vite Devtools 組み込み**: 開発ツールのビルトインオプション
- **TypeScript paths 自動解決**: `tsconfig.json` のパスエイリアスを設定不要で認識
- **Wasm SSR 対応**: サーバーサイドレンダリング環境での WebAssembly サポート
- **ブラウザコンソール転送**: ブラウザのログをターミナルに出力

## 破壊的変更・移行ガイド

### 動作要件

- **Node.js**: 20.19+ または 22.12+ が必須（18.x サポート終了）

### インストールサイズ

Vite 7 から約 15MB 増加：
- lightningcss の依存追加: 約 10MB
- Rolldown バイナリ: 約 5MB

### 移行手順

1. **推奨**: まず Vite 7 環境で `rolldown-vite` を導入して互換性を検証
2. Vite 8 にアップグレード（`npm install vite@latest`）
3. 多くのプロジェクトでは互換性レイヤーにより設定変更不要
4. カスタム Rollup プラグインを使用している場合は、Rolldown 互換性を個別に確認

### esbuild・Rollup プラグインの移行

- `esbuild` のトランスフォームオプションを直接使用していた場合は Rolldown の同等オプションに置き換え
- `rollupOptions` の大半はそのまま動作するが、一部内部 API に依存したプラグインは修正が必要

## 今後の注目点

- **Full Bundle Mode の安定化**: 現在実験的だが、開発サーバーのパフォーマンスをさらに改善する可能性
- **Rolldown 単体利用**: Vite 以外のツールチェーンからの Rolldown 直接利用の拡大
- **Oxc ツールチェーン統合**: Rolldown の基盤である Oxc（Rust ベースの JS ツールチェーン）のさらなる統合
- **VoidZero のエコシステム**: Vite を支える VoidZero 社による次世代 JavaScript ツールチェーンの発展
