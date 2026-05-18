# Bun — Zig→Rust リライト PR #30412 マージ

- **日付**: 2026-05-18
- **カテゴリ**: Backend / Runtime
- **ソース**: [The Register](https://www.theregister.com/devops/2026/05/14/anthropics-bun-rust-rewrite-merged-at-speed-of-ai/), [lilting.ch 解説記事](https://lilting.ch/en/articles/bun-zig-rust-ai-port), [Hacker News](https://news.ycombinator.com/item?id=48132488)

## 概要

JavaScript / TypeScript ランタイム Bun の Zig から Rust への大規模リライトが 2026 年 5 月 14 日に main へマージされた。PR #30412 は 6,755 コミット・2,188 ファイル変更・100 万行超の追加で、960,000 行の Zig コードが約 6 日間で Rust へ置き換えられた。コードの大半は Anthropic の Claude エージェントによって生成・修正されており、AI 駆動開発の規模感を示す象徴的なイベントとして大きな注目を集めている。

## 主な変更点

### ポートの規模

- **PR #30412**: 6,755 commits / 2,188 files changed / 1,009,257 行追加。
- 960,000 行の Zig → Rust ポート。
- バイナリサイズが 3–8MB 削減。
- Bun のテストスイートを全プラットフォームでパス（記事内では「99.8% パス」とも報告）。

### AI エージェントによる並行作業

複数の `claude/*` ブランチが同時に走り、それぞれ役割を分担した：

- `claude/phase-a-port` — メインのポート作業
- `claude/bench-until-green` — ベンチマークのチューニング
- `claude/code-dedup` — 5,000 行超の重複コードを統合
- `claude/ci-auto-fix-*` — CI 失敗の自動修正

これに加え CodeRabbit がコードレビューを担当し、生成→検証ループが回された。

### Zig からの離脱動機

Bun の作成者 Jarred Sumner はマージ後の説明で次のように述べている：

- 主目的は **パフォーマンスではなくメモリ安全性** 。Zig 時代の use-after-free / double-free を Rust のコンパイル時チェックで防ぐ。
- Zig コミュニティの **「no-AI」方針** が Bun チームの開発スタイル（AI 全面利用）と相容れない。
- 近年の Bun は Zig のフォークに独自パッチを当てて使っており、それらが upstream へマージできない状態だった。

## 破壊的変更・移行ガイド

エンドユーザーから見える破壊的変更は当面なし。

- 通常リリース版は **v1.3.14（最後の Zig 版）** のまま据え置き。
- Rust 版は **canary build** で先行利用可能：

  ```bash
  bun upgrade --canary
  ```

- 残作業として Phase B / C の最適化と cleanup PR が予定されており、これらが完了するまでは canary 限定。
- 既存のスクリプト・ライブラリ・`bun install` ワークフローはそのまま動作することがテストで確認されている。

## 今後の注目点

- **unsafe ブロックの整理**: 初期のポートでは Rust の `unsafe` ブロックが多用されている（Theo 氏らの解析で 13,000 個との報告もあり）。今後の cleanup でこれをどこまで削減できるかが「Rust に書き換えた価値」の試金石となる。
- **メンテナンスモデルの変化**: 長期メンテナンスを Anthropic が担う形になり、AI エージェントによるコード生成が標準ワークフローに組み込まれる。OSS のレビュー文化やコントリビューションフローへの影響は要観察。
- **コミュニティ反応**: HN や X では「Zig が悪かったわけではない」「AI 生成コードの安全性をどう担保するか」「Rust 化で得られるメモリ安全性のメリットは unsafe をどれだけ減らせるかに依存する」といった議論が続いている。
- **競合ランタイムへの波及**: Node.js / Deno / Bun の三つ巴で、AI 駆動の大規模リファクタリングを実プロダクトに適用した最初の例として、他プロジェクトの参考事例になる可能性。
