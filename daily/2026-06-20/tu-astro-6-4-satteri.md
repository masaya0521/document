# Astro — v6.4（Rust 製 Markdown プロセッサ Sätteri）

- **日付**: 2026-05-28（リリース）
- **カテゴリ**: Frontend
- **ソース**: [Astro Blog: Astro 6.4](https://astro.build/blog/astro-640/), [Astro 6.4 Deep Dive](https://needhelp.icu/blogs/astro-64-pluggable-markdown-satteri-cloudflare)

## 概要

Astro 6.4 の目玉は、**Rust 製の新しい Markdown / MDX パイプライン「Sätteri」**の導入。これまで Astro の Markdown 処理は JavaScript エコシステムの `unified`（remark / rehype）に依存していたが、ドキュメントサイトのような Markdown 主体の大規模サイトではビルド時間のボトルネックになりやすかった。

6.4 では新しい**プラガブルな `markdown.processor` API** が追加され、デフォルトの unified ベースパイプラインを丸ごと差し替えられるようになった。その差し替え先の一つとして提供されるのが Rust 実装の Sätteri で、`@astrojs/markdown-satteri` パッケージとして導入する。Astro 自身のドキュメントサイトと Cloudflare のドキュメントサイトで試したところ、いずれもビルド時間を 1 分以上短縮できたとされる。

## 主な変更点

### Sätteri — Rust 製 Markdown/MDX プロセッサ

- Markdown と MDX のパイプラインを Rust で実装し、ネイティブ速度で処理。
- `@astrojs/markdown-satteri` パッケージとして提供され、新しい processor API 経由で有効化する。
- Markdown が大量にあるドキュメント/ブログ系サイトでビルド時間を大幅短縮。

### プラガブルな markdown.processor API

- `markdown.processor` API により、デフォルトの unified ベースパイプラインを完全に差し替え可能に。
- 既存の remark / rehype プラグインは（unified を使い続ける限り）従来どおり動作する。
- 一方で、トップレベルの `markdown` 設定オプションは新 API への移行に伴い非推奨（deprecated）となった。

## 破壊的変更・移行ガイド

- **Sätteri は remark / rehype プラグインを実行しない**。unified エコシステムのプラグインに依存している場合は、次のいずれかが必要:
  1. 当面は従来の `unified()` プロセッサを使い続ける（Sätteri に切り替えない）。
  2. 依存プラグインを Sätteri の MDAST / HAST プラグインへ移植する。
- トップレベルの `markdown` 設定は非推奨化されたため、新しい `markdown.processor` API への移行が推奨される（即座の破壊ではないが将来的な対応が必要）。
- プラグイン非依存・Markdown が大量にあるサイトほど Sätteri 導入のメリットが大きく、移行コストも低い。

## 今後の注目点

- Sätteri の MDAST / HAST プラグイン API がどこまで充実し、unified エコシステムの主要プラグインが移植されていくか。
- 他のフレームワーク（Next.js / Nuxt 等）が Rust ベースの Markdown 処理に追随するか。Astro 6.4 はフロントエンドツールチェインの「Rust 化」トレンドの一例。
- プラガブル processor API が Markdown 以外のコンテンツ処理にも拡張されるかどうか。
