# Bun — 960K 行の Zig→Rust AI リライト

- **日付**: 2026-05-14（マージ日）
- **カテゴリ**: Backend / Language Runtime
- **ソース**: [The Register](https://www.theregister.com/devops/2026/05/14/anthropics-bun-rust-rewrite-merged-at-speed-of-ai/5240381), [Hacker News](https://news.ycombinator.com/item?id=48132488), [dasroot.net 分析](https://dasroot.net/posts/2026/05/bun-rust-rewrite-engineering-reality-unsafe-blocks-ai-migration/)

## 概要

JavaScript ランタイム Bun の実装言語が Zig から Rust へ変更された。100 万行超のコードが追加され、60 万行超の Zig コードが削除されるという大規模な言語移行であり、その大部分が AI（Anthropic の Claude Code）によって 6 日間で実行された点が大きな話題を呼んだ。

## 背景と動機

Bun は当初 Zig で実装されていたが、以下の要因から Rust への移行が決断された:

- **Zig コミュニティの AI ポリシー**: Zig は AI 生成コードの受け入れに消極的。Bun チームは AI を開発の中核に据えており、方針が相容れなくなった
- **Zig フォークの限界**: 最近の Bun は Zig の独自フォークを使用しており、上流へのコントリビューションが困難に
- **Rust エコシステムの優位性**: crates.io のエコシステム、メモリ安全性の保証、充実したツールチェインが魅力

## AI 駆動の移植プロセス

Bun 創設者の Jarred Sumner は「もう何ヶ月も自分たちでコードをタイプしていない」と述べ、Claude Code を主要な開発ツールとして使用していることを明かした。

- **960,000 行**のコードを AI エージェントが処理
- 所要期間は**わずか 6 日間**
- 「本質的に同じコードベース」の言語間移植という位置づけ

## テスト互換性

> "99.8 percent of bun's pre-existing test suite passes on Linux x64f glibc in the rust rewrite"

- 全プラットフォームでテストスイートをパス
- 一部のメモリリークが修正済み
- バイナリサイズが 3〜8 MB 縮小

## 懸念点と課題

### unsafe ブロック

Rust への移植で **13,000 の unsafe ブロック** が含まれている。Rust の安全性保証を部分的に迂回するこれらのブロックは、厳密な監査が必要。ランタイムの性質上、低レベル操作で unsafe が必要になる場面は多いが、その数の多さが議論を呼んでいる。

### メモリ安全性の限界

Rust のコンパイラは use-after-free や double-free を防ぐが、以下のケースは依然として課題:

- 参照保持（reference retention）によるメモリリーク
- JavaScript 境界のリエントリーに起因するリーク
- GC との相互作用における予期しない挙動

### コミュニティの反応

賛否両論の激しい反応:

- **懸念**: 100 万行超の diff を適切にレビューできるのか。AI 生成コードの品質保証をどう担保するのか
- **評価**: テストスイートの高い互換性は実用的な品質指標として有効
- **議論**: AI 駆動の大規模リライトは今後のソフトウェア開発のパラダイムを変えるか

## 今後の注目点

- 13,000 unsafe ブロックの段階的な削減・監査の進捗
- Rust 版 Bun のパフォーマンスベンチマーク（Zig 版との比較）
- 他の大規模プロジェクトが同様の AI 駆動リライトを試みるかどうか
- Zig コミュニティへの影響と、AI ポリシーを巡る OSS エコシステムの議論
