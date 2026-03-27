# Vite 8.0 — Rolldown 統合によるアーキテクチャ刷新

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [GitHub Releases](https://github.com/vitejs/vite/releases)

## 概要

Vite 8.0 は「Vite 2 以来で最も重要なアーキテクチャ変更」と位置づけられるメジャーリリース。開発時に esbuild、本番ビルドに Rollup という二重バンドラー構成を廃止し、VoidZero チームが開発した Rust ベースの統一バンドラー **Rolldown** に一本化した。これにより本番ビルド速度が 10〜30 倍向上し、開発と本番の動作差異も解消される。

## 主な変更点

### Rolldown 統合

Vite はこれまで開発時に esbuild（高速な変換）、本番ビルドに Rollup（最適化されたバンドル）という実用的な二重構成を採用していた。Vite 8 ではこれを Rolldown に統一：

- **Rolldown**: Rust で書かれたバンドラー。Rollup と同じプラグイン API をサポート
- **既存プラグインの互換性**: ほとんどの Vite プラグインがそのまま動作
- **互換性レイヤー**: 既存の `esbuild` / `rollupOptions` 設定を自動変換

### 実世界のパフォーマンス改善

| プロジェクト | 改善 |
|------------|------|
| Linear | 46秒 → 6秒（**87% 削減**） |
| Ramp | **57% 削減** |
| Mercedes-Benz.io | 最大 **38% 削減** |
| Beehiiv | **64% 削減** |

### 新機能

- **統合 Devtools**: `devtools` オプションでデバッグ・分析ツールを有効化
- **tsconfig paths 組込みサポート**: `resolve.tsconfigPaths: true` で TypeScript のパスエイリアス解決をネイティブ対応（若干のパフォーマンスコストあり）
- **Wasm SSR 対応**: `.wasm?init` インポートが SSR 環境でも動作
- **ブラウザコンソール転送**: ブラウザ側の `console.log` やエラーを dev サーバーのターミナルに転送。コーディングエージェントとの連携時に特に有用
- **`emitDecoratorMetadata` 自動対応**: 外部プラグイン不要

### @vitejs/plugin-react v6

- Babel 依存を廃止し、Oxc で React Refresh トランスフォームを実行
- インストールサイズを削減

## 破壊的変更・移行ガイド

### インストールサイズの増加

Vite 7 比で約 15 MB 増加：
- lightningcss: +10 MB（CSS 最小化の品質向上）
- Rolldown バイナリ: +5 MB（パフォーマンス最適化のトレードオフ）

### 移行のしやすさ

多くのプロジェクトでは設定変更不要。互換性レイヤーが既存の esbuild・rollupOptions 設定を自動変換する。段階的な移行パスも提供されている。

### システム要件

- Node.js 20.19+ / 22.12+（Vite 7 と同一）

## 今後の注目点

- **Rolldown の安定化**: ベータ期間中に RC まで進行しており、今後さらなる安定化・最適化が見込まれる
- **エコシステムの対応**: Tailwind CSS が早速 `@tailwindcss/vite` で Vite 8 対応を完了（[PR #19790](https://github.com/tailwindlabs/tailwindcss/pull/19790)）
- **Oxc ベースのツールチェーン**: Rolldown + Oxc による Rust ベース JavaScript ツールチェーンの統合が進行中
- **プラグイン互換性**: 大半は互換だが、esbuild 固有の機能に依存するプラグインは Rolldown 対応が必要になる場合がある
