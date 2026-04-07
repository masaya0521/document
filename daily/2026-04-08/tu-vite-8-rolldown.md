# Vite 8.0 — Rolldown 統合によるアーキテクチャ刷新

- **日付**: 2026-03-12（正式リリース）
- **カテゴリ**: Build Tool
- **ソース**: [公式ブログ](https://vite.dev/blog/announcing-vite8), [Beta 発表](https://vite.dev/blog/announcing-vite8-beta), [GitHub Releases](https://github.com/vitejs/vite/releases)

## 概要

Vite 8.0 は、Vite 2 以来最大のアーキテクチャ変更をもたらすリリースである。これまで開発時は esbuild、本番ビルドは Rollup という二重バンドラー構成だったものを、VoidZero 開発の Rust 製バンドラー **Rolldown** に統一した。ビルド速度は Rollup 比で 10-30 倍に向上し、週間 6,500 万ダウンロードを超えるエコシステムに大きなインパクトを与えている。

## 主な変更点

### Rolldown 統合

Rolldown は 3 つの設計目標で開発された。

1. **パフォーマンス**: Rust によるネイティブ速度で動作し、Rollup 比 10-30x の高速化
2. **互換性**: Rollup と同じプラグイン API をサポートし、既存プラグインとの互換性を維持
3. **高度な機能**: Full Bundle Mode、柔軟なチャンク分割、モジュール永続キャッシング

### 実プロジェクトでのパフォーマンス改善

複数の企業が大幅な改善を報告している。

| 企業 | 改善結果 |
|---|---|
| Linear | 46 秒 → 6 秒 |
| Beehiiv | 64% 削減 |
| Mercedes-Benz.io | 最大 38% 削減 |

### Full Bundle Mode（実験的）

開発時にも本番同様のバンドルを行うモード。初期計測では以下の改善が見込まれている。

- dev サーバー起動: **3x 高速化**
- フルリロード: **40% 高速化**
- ネットワークリクエスト: **10x 削減**

大規模プロジェクトでのスケーラビリティ向上が主な狙い。

### Vite Devtools

新しい `devtools` オプションにより、開発者向けのデバッグ・分析ツールを有効化できるようになった。

### Plugin Registry

[registry.vite.dev](https://registry.vite.dev) が公開され、Vite・Rolldown・Rollup のプラグインを検索できるディレクトリが提供されている。npm から日次でプラグインデータを収集している。

## 破壊的変更・移行ガイド

### 動作環境

- **Node.js 20.19+ または 22.12+** が必要

### インストールサイズ

Vite 8 では約 **15MB のサイズ増加** がある。内訳は以下の通り。

- lightningcss: 約 10MB
- Rolldown: 約 5MB

### 移行の容易さ

Rolldown の互換レイヤーにより、多くのプロジェクトでは **設定変更なし** で移行可能。ただし、Rollup プラグインを多用する複雑なプロジェクトでは段階的な移行が推奨される。

```bash
# アップデート
npm install vite@latest

# 動作確認
npx vite build
```

## 今後の注目点

- **Full Bundle Mode の安定化**: 実験的フラグから正式機能への昇格時期
- **Rolldown 単体利用**: Vite 外での Rolldown 直接利用のエコシステム拡大
- **Oxc との統合**: 同じく VoidZero が開発する Rust 製 JavaScript ツールチェーン Oxc（パーサー・リンター・トランスフォーマー）との統合深化
- **esbuild / Rollup プラグインの移行状況**: エコシステム全体でのプラグイン互換性の成熟度
