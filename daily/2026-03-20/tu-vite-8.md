# Vite 8.0 — Rolldown統合による統一バンドラー時代

- **日付**: 2026-03-12
- **カテゴリ**: Build Tool / Frontend
- **ソース**: [Vite Blog](https://vite.dev/blog/announcing-vite8), [Vite 8 Beta](https://vite.dev/blog/announcing-vite8-beta), [GitHub Releases](https://github.com/vitejs/vite/releases)

## 概要

Vite 8.0 は Vite 2 以来最も大きなアーキテクチャ変更を伴うリリースである。従来の esbuild（開発用）+ Rollup（本番用）の二重バンドラー構成から、Rust 製の統一バンドラー「Rolldown」への移行を完了した。ビルド速度は Rollup 比で10-30倍高速化し、プラグイン互換性も維持されている。

## 主な変更点

### Rolldown 統合

Vite 8 の最大の変更点は、Rolldown を単一の統一バンドラーとして採用したこと。Rolldown は Rollup と同じプラグイン API をサポートしており、既存の Vite プラグインの多くがそのまま動作する。

**パフォーマンス実績（実プロジェクト）:**

| プロジェクト | 改善率 |
|-------------|--------|
| Linear | 87%削減（46秒 → 6秒） |
| Ramp | 57%短縮 |
| Beehiiv | 64%削減 |

統一バンドラーにより、以下の機能が新たに可能になった:
- フルバンドルモード
- より柔軟なチャンク分割
- モジュールレベルの永続キャッシュ
- Module Federation サポート

### 新機能

- **Vite Devtools 統合**: `devtools` オプションでデバッグ・分析ツールを有効化可能
- **TypeScript tsconfig paths サポート**: `resolve.tsconfigPaths: true` で TypeScript パスエイリアス解決を有効化（パフォーマンスコストがあるためデフォルト無効）
- **emitDecoratorMetadata 対応**: TypeScript のデコレータメタデータの自動サポートが組み込まれ、外部プラグインが不要に
- **Wasm SSR サポート**: `.wasm?init` インポートが SSR 環境で動作するように
- **ブラウザコンソール転送**: ブラウザのコンソールログ/エラーを dev サーバーのターミナルに転送。コーディングエージェントとの連携で特に有用
- **Vite Plugin Registry**: [registry.vite.dev](https://registry.vite.dev) を公開。Vite / Rolldown / Rollup のプラグインを検索可能

### パッケージサイズ

Vite 7 比で約15MB増加:
- lightningcss: 約10MB（CSS最小化の改善）
- Rolldown: 約5MB

## 破壊的変更・移行ガイド

### Node.js 要件

Node.js 20.19+ または 22.12+ が必要（Vite 7 と同じ）。

### 推奨移行手順

二段階の移行が推奨されている:

1. **Vite 7 環境で `rolldown-vite` パッケージをテスト**: 既存の Vite 7 プロジェクトで Rolldown バンドラーの互換性を確認
2. **Vite 8 へアップグレード**: 互換性が確認できたら Vite 8 にアップグレード

多くのプロジェクトでは設定変更不要で移行できるが、複雑な Rollup プラグインや高度なビルド設定を持つプロジェクトは[移行ガイド](https://vite.dev/guide/migration)の確認が必要。

### Tailwind CSS との連携

Vite 8.0 リリース当日に `@tailwindcss/vite` が Vite 8 対応をマージ。peer dependency を `^8.0.0` に拡張し、統合テストも追加済み。

## 今後の注目点

- Rolldown の安定化と残存する互換性の問題の解消
- Module Federation の実用化とマイクロフロントエンドへの影響
- モジュールレベル永続キャッシュによる CI/CD パイプラインの高速化
- エコシステム全体（Next.js、Nuxt、SvelteKit 等）の Vite 8 対応状況
- Vite Plugin Registry の成長とプラグインエコシステムの活性化
