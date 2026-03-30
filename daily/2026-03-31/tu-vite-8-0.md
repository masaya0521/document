# Vite 8.0 — Rolldown 統合による統一バンドラーアーキテクチャ

- **日付**: 2026-03-31
- **カテゴリ**: Build Tool
- **ソース**: [Vite Blog](https://vite.dev/blog/announcing-vite8), [GitHub Releases](https://github.com/vitejs/vite/releases)

## 概要

Vite 8.0 は 2026年3月12日にリリースされた、Vite 2 以降で最も大きなアーキテクチャ変更を含むメジャーバージョンである。開発時に esbuild、本番ビルドに Rollup という従来の二重バンドラー構成を廃止し、Rust 製の統一バンドラー **Rolldown** に一本化した。これにより 10-30 倍のビルド高速化を実現しつつ、既存プラグインとの高い互換性を維持している。

## 主な変更点

### Rolldown 統合
Vite 8 の中核となる変更。Rolldown は以下の 3 つの目標を掲げて開発された：

- **パフォーマンス**: Rollup 比 10-30 倍高速、esbuild 同等の速度
- **互換性**: 既存の Vite プラグインの大半がそのまま動作
- **高度な機能**: フルバンドルモード、柔軟なチャンク分割、永続キャッシュ、Module Federation 対応

### 実測パフォーマンス

複数の企業が大幅な改善を報告：

| 企業 | 改善結果 |
|------|---------|
| Linear | 46秒 → 6秒 |
| Ramp | 57% 削減 |
| Beehiiv | 64% 削減 |

### Vite Devtools
新しい `devtools` オプションにより、開発時のデバッグ・分析ツールを有効化できる。

### @vitejs/plugin-react v6
Vite 8 と同時リリース。React Refresh トランスフォームに Oxc を採用し、Babel への依存を完全に排除。インストールサイズが縮小。

### プラグインレジストリ
`registry.vite.dev` として新たに公開。Vite・Rolldown・Rollup 向けプラグインの検索可能なディレクトリ。

### その他の新機能
- TypeScript tsconfig `paths` のネイティブサポート
- デコレータメタデータの自動対応
- WebAssembly SSR サポート
- ブラウザコンソールの転送機能

## 破壊的変更・移行ガイド

### Node.js 要件
Node.js 20.19+ または 22.12+ が必須（Vite 7 と同じ要件）。

### インストールサイズ
約 15MB 増加（lightningcss: 10MB、Rolldown: 5MB）。

### 移行パス
互換性レイヤーにより、多くのプロジェクトでは設定変更なしで移行可能。複雑なプロジェクトでは段階的な移行が推奨される：

1. Vite 8 にアップグレード
2. 既存のビルドが正常に動作することを確認
3. カスタムプラグインがある場合は Rolldown 互換性を検証
4. パフォーマンスのベンチマークを比較

### 注意点
- Rollup 固有の低レベル API を直接使用しているプラグインは調整が必要な場合がある
- 永続キャッシュはオプトインで利用可能

## 今後の注目点

- Rolldown のさらなる最適化と機能追加
- Module Federation の本番利用事例の拡大
- エコシステム全体（Next.js 以外のフレームワーク）での Vite 8 対応状況
- Turbopack との競争の行方（Next.js エコシステム vs Vite エコシステム）
