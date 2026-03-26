# Vite 8.0 — Rolldown 統一バンドラーによるアーキテクチャ刷新

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [The Register](https://www.theregister.com/2026/03/16/vite_8_rolldown/)

## 概要

Vite 8.0 は Vite 2 以来最大のアーキテクチャ変更を含むメジャーリリースである。従来の esbuild（開発環境）+ Rollup（本番ビルド）という二重バンドラー構成を廃止し、Rust ベースの **Rolldown** を単一の統一バンドラーとして採用。これにより開発環境と本番環境の一貫性が向上し、ビルド速度は Rollup 比で 10〜30 倍の高速化を達成した。

## 主な変更点

### Rolldown 統一バンドラー

Vite 8 の中核となる変更。VoidZero チームが開発した Rust ベースのバンドラー Rolldown が、esbuild と Rollup の両方を置き換える。

**アーキテクチャの変遷:**
- Vite 2〜7: esbuild（dev 高速トランスパイル）+ Rollup（prod 最適化ビルド）
- Vite 8: Rolldown 一本化（dev / prod 両方）

**メリット:**
- 単一の変換パイプラインにより dev と prod の動作差異が解消
- Rollup 互換のプラグイン API をサポート（既存プラグインの移行が容易）
- フルバンドルモード、モジュール永続キャッシング、Module Federation 等の新機能が実現可能に

### パフォーマンス改善（実測値）

各企業からの報告:

| 企業 | 改善結果 |
|------|---------|
| Linear | 46 秒 → 6 秒 |
| Ramp | 57% 削減 |
| Mercedes-Benz.io | 最大 38% 削減 |
| Beehiiv | 64% 削減 |

ベンチマーク上は Rollup 比で **10〜30 倍高速**（esbuild と同等レベル）。

### 新機能

- **統合 Devtools**: 開発サーバーに組み込みの開発者ツール
- **TypeScript `tsconfig paths` サポート**: `tsconfig.json` のパスマッピングを自動認識
- **`emitDecoratorMetadata` 自動サポート**: デコレータメタデータの自動生成
- **WebAssembly SSR サポート**: Wasm を使った SSR が可能に
- **ブラウザコンソール転送**: ブラウザのコンソール出力をターミナルに転送

### インストールサイズ

Vite 7 比で約 15MB 増加:
- lightningcss 統合: 約 10MB
- Rolldown バイナリ: 約 5MB

### Node.js 要件

Node.js 20.19+ または 22.12+ が必要（Vite 7 と同じ）。

## 破壊的変更・移行ガイド

### 段階的移行（推奨）

複雑なプロジェクトでは段階的なアプローチが推奨される:

```bash
# ステップ 1: Vite 7 のまま rolldown-vite パッケージでテスト
npm install rolldown-vite

# ステップ 2: vite.config.ts で rolldown-vite を使用してビルド検証

# ステップ 3: 問題なければ Vite 8 にアップグレード
npm install vite@8
```

### プラグイン互換性

Rolldown は Rollup と同じプラグイン API をサポートするが、一部のプラグインで動作差異が生じる可能性がある。公式の互換性リストを確認すること。

### esbuild 依存コードの確認

直接 esbuild の API を利用しているカスタム設定がある場合、Rolldown の API に移行が必要。

## 今後の注目点

- **Rolldown + Oxc エコシステム**: Vite（ビルドツール）+ Rolldown（バンドラー）+ Oxc（コンパイラ）という Rust ベースの統合ツールチェーンが形成されつつある
- **Module Federation**: Rolldown ネイティブの Module Federation サポートにより、マイクロフロントエンドの構築が容易になる可能性
- **永続キャッシング**: モジュール単位の永続キャッシュによるインクリメンタルビルドのさらなる高速化
- **エコシステム対応**: Next.js（Turbopack）との競合構図。Nuxt / SvelteKit / Astro 等は Vite ベースのため直接恩恵を受ける
