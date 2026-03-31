# Vite 8.0 — Rolldown 統合による統一バンドラー

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [The Register](https://www.theregister.com/2026/03/16/vite_8_rolldown/)

## 概要

Vite 8.0 は Vite 2 以来最大のアーキテクチャ変更となるリリース。開発時に esbuild、本番ビルドに Rollup という二重バンドラー構成を廃止し、Rust 製の単一バンドラー **Rolldown** に統合した。これにより開発と本番の挙動差異が解消され、ビルド速度は 10-30x 向上。既存の Vite プラグインの大半はそのまま動作する。

## 主な変更点

### Rolldown 統合

Rolldown は Rollup 互換の API を持つ Rust 製バンドラー。単一バンドラーへの統合により以下が実現:

- **パフォーマンス**: ネイティブ速度で動作し、Rollup 比で 10-30x 高速
- **一貫性**: 開発と本番で同一のバンドラーを使用し、挙動差異を解消
- **新機能**: Full Bundle Mode、柔軟なチャンク分割、モジュールレベル永続キャッシュ、Module Federation サポート

**実際の導入企業でのパフォーマンス実績:**

| 企業 | 改善内容 |
|------|---------|
| Linear | 46秒 → 6秒（約 87% 削減） |
| Ramp | 57% ビルド時間削減 |
| Mercedes-Benz.io | 最大 38% 削減 |
| Beehiiv | 64% 削減 |

### Vite DevTools 統合

`devtools` オプションでビルド分析・デバッグツールを有効化可能。

### TypeScript paths 自動解決

`tsconfig.json` の `paths` エイリアスをネイティブサポート。`vite-tsconfig-paths` プラグインが不要に。

### emitDecoratorMetadata 対応

外部プラグインなしでデコレータメタデータの出力に対応。

### Wasm SSR サポート

サーバーサイドレンダリング環境での WebAssembly 処理をサポート。

### ブラウザコンソール転送

クライアント側の `console.log` やエラーを開発サーバーのターミナルに転送表示。

### Full Bundle Mode（実験的）

開発時にもモジュールをバンドルするモード。予備的な結果:
- 開発サーバー起動: 3x 高速化
- フルリロード: 40% 高速化
- ネットワークリクエスト: 10x 削減

## 破壊的変更・移行ガイド

### 動作要件

- **Node.js 20.19+ または 22.12+** が必須（旧バージョンはサポート外）

### プラグイン互換性

既存の Vite プラグインの大半は Vite 8 でそのまま動作する。Rolldown は Rollup 互換の Plugin API を持つため、移行コストは最小限。

### インストールサイズ

Vite 7 比で約 15MB 増加（Rolldown 約 5MB + lightningcss 約 10MB）。

### 移行手順

1. Node.js を 20.19+ または 22.12+ に更新
2. `npm install vite@8` で更新
3. `vite-tsconfig-paths` を使っている場合は削除を検討（ネイティブサポートに置換）
4. カスタム Rollup プラグインを使っている場合は動作確認

## 今後の注目点

- **Full Bundle Mode** の安定化（開発体験の大幅な改善が期待）
- **Raw AST アクセス**: プラグインからの低レベル AST 操作
- **Native MagicString**: Rust ベースの文字列変換によるさらなる高速化
- Rolldown 自体の継続的改善（Oxc パーサーとの統合深化）
