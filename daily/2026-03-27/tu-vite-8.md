# Vite 8.0 — Rolldown による統一バンドラーアーキテクチャ

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [The Register](https://www.theregister.com/2026/03/16/vite_8_rolldown/)

## 概要

Vite 8.0 は、開発時の esbuild と本番ビルドの Rollup という二重バンドラー構成を廃止し、Rust 製の統一バンドラー **Rolldown** に一本化した。Vite 2 以来最大のアーキテクチャ変更であり、ビルド速度は 10-30x 向上する。

## 主な変更点

### Rolldown 統一バンドラー

- 開発・本番の両方で Rolldown を使用する統一アーキテクチャ
- Rollup と同じプラグイン API をサポートし、既存プラグインはほぼ設定変更なしで動作
- `esbuild` と `rollupOptions` の互換性レイヤーによる自動変換

### パフォーマンス改善（実企業の報告値）

| 企業 | 改善幅 |
|------|--------|
| Linear | 46s → 6s（約 87% 削減） |
| Ramp | 57% 削減 |
| Mercedes-Benz.io | 最大 38% 削減 |
| Beehiiv | 64% 削減 |

### 新機能

- **Devtools オプション**: `devtools` オプションで Vite Devtools を有効化し、デバッグ・分析ツールを統合
- **registry.vite.dev**: Vite / Rolldown / Rollup プラグインの検索可能なディレクトリ
- **tsconfig paths サポート**: TypeScript のパスマッピングをネイティブサポート（設定可能）
- **`emitDecoratorMetadata`**: 組み込みサポート
- **SSR 環境での Wasm 対応**
- **ブラウザコンソール転送機能**

### @vitejs/plugin-react v6

Vite 8 と同時にリリース。Oxc ベースの React Refresh 変換を採用し、Babel 依存を完全に除去。

### インストールサイズ

Vite 7 比で約 15MB 増加：
- lightningcss: 約 10MB（CSS 最適化向上）
- Rolldown: 約 5MB

### Node.js 要件

Node.js 20.19+ / 22.12+（Vite 7 と同じ）

## 破壊的変更・移行ガイド

- esbuild から Rolldown への移行に伴い、一部のビルド挙動に差異が生じる可能性あり
- 大規模プロジェクトでは段階的移行を推奨：Vite 7 で `rolldown-vite` パッケージを先に試してから Vite 8 に移行
- `rollupOptions` と `esbuild` オプションは互換性レイヤーで自動変換されるが、高度なカスタマイズを行っている場合は検証が必要

## 今後の注目点

- **Full Bundle Mode（実験的）**: 開発時にもモジュールをバンドルするモード。初期結果では dev サーバー起動 3x 高速化、フルリロード 40% 高速化、ネットワークリクエスト 10x 削減
- Rolldown 自体の継続的なパフォーマンス改善
- エコシステム全体（Tailwind CSS、各フレームワーク等）の Vite 8 対応状況
