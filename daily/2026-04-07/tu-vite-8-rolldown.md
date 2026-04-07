# Vite 8.0 — Rolldown 統合による 10-30x 高速化

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [The Register](https://www.theregister.com/2026/03/16/vite_8_rolldown/)

## 概要

Vite 8.0 は、Vite 2 以来最大のアーキテクチャ変更となるリリースである。従来の開発時 esbuild + 本番 Rollup という二重構造を廃止し、Rust 製の統一バンドラー「Rolldown」に一本化した。これにより本番ビルドが 10-30x 高速化され、開発/本番環境の挙動の一貫性が大幅に向上した。

## 主な変更点

### Rolldown 統合

Rolldown は Rollup 互換の API を持つ Rust 製バンドラーで、以下の 3 つの設計目標を掲げている:

1. **パフォーマンス**: ネイティブコードによる高速処理
2. **互換性**: 既存の Rollup プラグインとの互換性維持
3. **高度な機能**: Module Federation、モジュール連携キャッシング等

### 実測パフォーマンス

| プロジェクト | 改善率 | 詳細 |
|------------|--------|------|
| Linear | 87% 削減 | 46s → 6s |
| Ramp | 57% 削減 | - |
| Mercedes-Benz.io | 38% 削減 | - |
| Beehiiv | 64% 削減 | - |

### 新機能

- **Vite Devtools 統合**: デバッグ・分析機能の組み込み
- **tsconfig paths 対応**: `resolve.tsconfigPaths` で有効化可能（プラグイン不要）
- **emitDecoratorMetadata**: TypeScript デコレータメタデータの自動サポート
- **Wasm SSR 対応**: サーバーサイドレンダリング環境での WebAssembly 機能拡張
- **ブラウザコンソール転送**: クライアント側エラーをターミナルに表示

### @vitejs/plugin-react v6

Babel から Oxc ベースに移行。Babel 依存を排除し、インストールサイズを削減。

## 破壊的変更・移行ガイド

### Node.js 要件

Node.js 20.19+ または 22.12+ が必要。

### インストールサイズの増加

約 15MB の増加:
- lightningcss: ~10MB（オプション → 標準依存に昇格）
- Rolldown バイナリ: ~5MB

### 互換性レイヤー

既存の `esbuild` および `rollupOptions` 設定は互換性レイヤーにより自動変換される。ただし、Rollup プラグインの一部で非互換が生じる可能性がある。

### 推奨される移行手順

段階的アプローチが推奨されている:

1. **Vite 7 のまま** `rolldown-vite` パッケージに切り替え、バンドラー変更の影響を分離して確認
2. 問題がなければ **Vite 8 にアップグレード**

この手順により、バンドラー変更による問題と Vite 本体のアップデートによる問題を切り分けられる。

## 今後の注目点

- **Full Bundle Mode（実験版）**: 開発時にも本番同様のバンドルを実施。予備結果では 3x 高速なサーバー起動、40% 高速なリロード、10x 削減のネットワークリクエスト
- **Raw AST transfer**: Rust 製 AST への低遅延アクセス
- **Native MagicString transforms**: Rust 計算を活用した JavaScript ロジック
- **Environment API 安定化**: Astro 6 等のフレームワークとの協調体制強化
- **Rolldown 単体利用**: 現時点では Vite 経由でのみ利用可能だが、将来的にスタンドアロン利用も検討中
