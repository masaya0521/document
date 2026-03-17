# Vite 8.0 — Rolldown 統合によるビルド革命

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [Vite Blog](https://vite.dev/blog/announcing-vite8), [The Register](https://www.theregister.com/2026/03/16/vite_8_rolldown/)

## 概要

Vite 8.0 は、開発時に esbuild・本番ビルドに Rollup という従来のデュアルバンドラー構成を廃止し、Rust 製の統合バンドラー **Rolldown** に一本化した。Vite 2 以来最大のアーキテクチャ変更であり、ビルド速度は 10-30 倍の高速化を実現。Rollup 互換のプラグイン API を維持しているため、既存プラグインの多くがそのまま動作する。

## 主な変更点

### Rolldown への統一

- esbuild（開発）と Rollup（本番）の 2 つのバンドラーを、Rust 製の **Rolldown** に統一
- Rolldown は Rollup 互換のプラグイン API をサポートし、ネイティブコードの速度で動作
- 単一バンドラーにより、開発と本番の挙動差異が解消

### パフォーマンス実績

企業による実測値:

| 企業 | 改善幅 |
|------|--------|
| Linear | 46s → 6s（約87%削減） |
| Ramp | 57% 削減 |
| Mercedes-Benz.io | 最大 38% 削減 |
| Beehiiv | 64% 削減 |

### 新機能

- **統合 Devtools**: 開発時のデバッグ・パフォーマンス計測ツールを内蔵
- **TypeScript `tsconfig paths` の組み込みサポート**: 追加プラグイン不要でパスエイリアスが動作
- **`emitDecoratorMetadata` の自動サポート**: TypeScript デコレータメタデータの自動処理
- **Wasm SSR サポート**: WebAssembly によるサーバーサイドレンダリング
- **ブラウザコンソール転送**: ブラウザのコンソール出力をターミナルに転送
- **フルバンドルモード**: 統一バンドラーだからこそ可能な新しいバンドル戦略
- **モジュールレベル永続キャッシュ**: ビルドキャッシュの粒度がモジュール単位に
- **Module Federation サポート**: マイクロフロントエンド向け機能

### Oxc コンパイラとの統合

Vite 8 により、ビルドツール（Vite）、バンドラー（Rolldown）、コンパイラ（Oxc）がエンドツーエンドで連携するツールチェーンが完成。パース・解決・変換・ミニファイまで一貫した動作が保証される。

## 破壊的変更・移行ガイド

- **Node.js 要件**: 20.19+ または 22.12+（Vite 7 と同じ）
- **インストールサイズ**: Vite 7 比で約 15MB 増加（lightningcss 約 10MB、Rolldown 約 5MB）
- **互換性レイヤー**: 設定の互換レイヤーが用意されており、多くのプロジェクトは設定変更なしでアップグレード可能
- **プラグイン互換性**: Rollup 互換 API のため、大半の既存プラグインはそのまま動作。一部のプラグインは Rolldown 固有の差異に対応が必要な場合あり

### アップグレード手順

```bash
# パッケージ更新
npm install vite@^8.0.0

# 既存設定の互換性確認
npx vite build
```

## 今後の注目点

- Rolldown の安定性向上とエッジケース対応の進展
- Rolldown 固有の最適化機能（persistent caching、Module Federation）の成熟度
- エコシステム全体の Vite 8 対応状況（Tailwind CSS は対応済み、各フレームワークの対応が進行中）
- Oxc コンパイラの単体利用や他ツールとの統合の動向
