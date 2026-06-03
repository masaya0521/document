# Deno — 2.8 リリース

- **日付**: 2026-05-22
- **カテゴリ**: Backend / Runtime
- **ソース**: [Deno Blog — Deno 2.8](https://deno.com/blog/v2.8), [denoland/deno Releases](https://github.com/denoland/deno/releases)

## 概要

Deno 2.8 は、TC39 の **`import defer` 提案**への対応と、開発ワークフローを補完する **6 つの新サブコマンド**を中心とした機能拡張リリース。npm エコシステムとの統合をさらに深め、cold npm install が従来比 3.66 倍（906ms vs 3,319ms）に高速化された点が実務上のインパクトとして大きい。

Node.js 互換性も継続的に強化され、内部テストスイートの合格率が 42% から 76.4% へ大幅に向上。CLI で npm パッケージを `npm:` プレフィックスなしにデフォルトで解決できるようになるなど、「Node からの移行コスト」を下げる方向に振り切っている。

## 主な変更点

### 新サブコマンド

- **`deno audit fix`**: 脆弱性のある npm パッケージをパッチ済みバージョンへ自動アップグレード。
- **`deno bump-version`**: 設定ファイルの version フィールドを更新（workspace 対応）。
- **`deno ci`**: frozen lockfile による再現性のあるインストール。CI 環境向け。
- **`deno pack`**: Deno / JSR プロジェクトから npm 公開可能な tarball をビルド。
- **`deno transpile`**: TypeScript の型を除去して JavaScript を出力。
- **`deno why`**: パッケージの依存チェーン（npm / JSR）を説明。

### モジュールロード

- **`import defer`**（TC39 提案）をサポート。モジュールは「export のいずれかに初めて触れたとき」に初めて評価される遅延評価が可能になり、起動コストを削減できる。

### パフォーマンス

- cold npm install が **3.66 倍**高速化。
- base64 エンコードが 3.07 倍、`node:http` のスループットが 2.21 倍向上。

### 開発ツール

- Chrome DevTools から Deno のネットワークトラフィックを inspect 可能に。
- 組み込み CPU プロファイラが複数フォーマット（V8 profile / flamegraph SVG / Markdown レポート）に対応。

### パッケージ管理

- CLI で npm パッケージがデフォルト解決（`npm:` プレフィックス不要）。
- monorepo 向けの catalog プロトコル。
- `--os` / `--arch` によるクロスプラットフォームインストール、`--prod` による production-only インストール。

## 破壊的変更・移行ガイド

- 大きな破壊的変更は告知されていないが、`npm:` プレフィックスのデフォルト解決により、既存スクリプトのインポート解決挙動が変わる可能性がある。lockfile を伴う CI では新設の `deno ci` への置き換えを検討するとよい。

## 今後の注目点

- Node.js 互換性合格率（76.4%）のさらなる向上と、Node からの移行事例の増加。
- `import defer` を活用した起動最適化が、サーバーレス / エッジ環境でどこまで効くか。
- `deno pack` / `deno audit fix` による npm 公開・セキュリティ運用の Deno 内完結。
