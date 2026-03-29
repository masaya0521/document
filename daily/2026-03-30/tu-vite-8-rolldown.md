# Vite 8.0 — Rolldown による統一バンドラーへの移行

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool
- **ソース**: [Vite Blog](https://vite.dev/blog/announcing-vite8), [The Register](https://www.theregister.com/2026/03/16/vite_8_rolldown/)

## 概要

Vite 8.0 は Vite 2 以来最大のアーキテクチャ変更となるリリース。これまで開発時は esbuild、本番ビルドは Rollup という二重バンドラー構成だったが、Rust 製の統一バンドラー **Rolldown** に一本化された。Rolldown は VoidZero チームが開発し、Rollup/Vite 互換のプラグイン API を維持しつつ、ネイティブ速度での動作を実現する。

統一バンドラーにより、フルバンドルモード、柔軟なチャンク分割、モジュールレベルの永続キャッシング、Module Federation サポートなど、これまで二重構成では困難だった機能が解禁された。

## 主な変更点

### Rolldown 統一バンドラー

- **パフォーマンス**: Rollup 比で 10〜30x 高速。esbuild と同等のパフォーマンスレベル
- **プラグイン互換**: Rollup・Vite 既存プラグインとの互換性を維持
- **新機能**: フルバンドルモード、柔軟なチャンク分割、モジュールレベル永続キャッシング、Module Federation

### 実プロジェクトでの成果

| プロジェクト | 改善 |
|---|---|
| Linear | 46 秒 → 6 秒 |
| Ramp | 57% 削減 |
| Mercedes-Benz.io | 最大 38% 削減 |
| Beehiiv | 64% 削減 |

### その他の改善

- 組み込みの tsconfig paths サポート
- TypeScript の `emitDecoratorMetadata` オプション対応
- [registry.vite.dev](https://registry.vite.dev) — Vite/Rolldown/Rollup プラグインの検索ディレクトリを新設

### インストールサイズ

約 15MB 増加（lightningcss 約 10MB、Rolldown 約 5MB）

## 破壊的変更・移行ガイド

大半のプロジェクトではスムーズにアップグレード可能とされている。

- `esbuild` および `rollupOptions` の設定は自動変換される
- 段階的な移行が推奨されており、先に `rolldown-vite` パッケージ経由で検証可能
- esbuild を直接利用していたカスタム設定がある場合は、Rolldown 互換の設定への書き換えが必要

```bash
# アップグレード
npm install vite@8

# 段階的移行（先行検証）
npm install rolldown-vite
```

## 今後の注目点

- Rolldown 1.0 正式リリース（現在は RC 段階）
- Vite のエコシステム全体での Rolldown 移行状況
- esbuild からの完全移行に伴うエッジケースの解消
- Module Federation の実運用事例の蓄積
