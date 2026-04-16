# Vite 8.0 — Rolldown による Rust ベースアーキテクチャ刷新

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [Vite 8 Beta アナウンス](https://vite.dev/blog/announcing-vite8-beta)

## 概要

Vite 8.0 は、これまで開発時に esbuild、プロダクションビルドに Rollup と分かれていた2つのバンドラーを、Rust 製の統一バンドラー **Rolldown** に置き換えた大規模なアーキテクチャ刷新リリースである。VoidZero（Evan You が設立）が開発する Rolldown は Rollup 互換のプラグイン API を持ち、既存の Vite プラグインの多くがそのまま動作する。

ビルド速度は Rollup 比で 10-30x 高速化され、実プロダクト環境でも大幅な改善が報告されている。

## 主な変更点

### Rolldown 統合

- **統一バンドラー**: 開発時とプロダクションビルドで同一のバンドラーを使用。dev/prod 間の挙動差異が解消
- **Rust ベース**: ネイティブ速度で動作し、esbuild 同等のパフォーマンスを実現
- **プラグイン互換**: Rollup / Vite プラグイン API をそのまま利用可能

### 実プロダクト環境でのパフォーマンス

| プロダクト | ビルド時間短縮 |
|-----------|-------------|
| Linear | 46秒 → 6秒 |
| Ramp | 57% 削減 |
| Mercedes-Benz.io | 最大 38% 削減 |
| Beehiiv | 64% 削減 |

### 新機能

- **統合 DevTools**: 開発体験の向上
- **TypeScript paths 自動解決**: `tsconfig.json` の `paths` をプラグインなしで解決
- **Decorator metadata サポート**: TC39 decorator の metadata 対応
- **Wasm SSR 対応**: WebAssembly を使ったサーバーサイドレンダリング

## 破壊的変更・移行ガイド

### 必須要件

- **Node.js 20.19+ または 22.12+** が必要（Node.js 18 以前は非サポート）
- インストールサイズが約 15MB 増加（lightningcss 約 10MB + Rolldown 約 5MB）

### 設定の移行

- `esbuild` オプションと `rollupOptions` の設定は自動変換機能で対応可能
- 段階的移行が推奨される場合あり
- 多くの既存プロジェクトでは `vite.config.ts` の変更なしで動作

### 移行手順

1. `package.json` で `vite` を `^8.0.0` に更新
2. Node.js バージョンを確認（20.19+ / 22.12+）
3. ビルド実行して互換性を確認
4. カスタム Rollup プラグインがある場合は動作検証

## 今後の注目点

- **Rolldown 1.0 正式リリース**: 現在は RC 段階。Vite 外での単体利用も可能に
- **Oxc 統合**: VoidZero が開発する Rust 製の JavaScript パーサー・リンター。将来の Vite バージョンでの統合が見込まれる
- **エコシステム波及**: Rolldown の Rust ベースアーキテクチャは、esbuild・Rollup・Webpack からの移行先として注目。Rust による JavaScript ツールチェーン統一の流れが加速
