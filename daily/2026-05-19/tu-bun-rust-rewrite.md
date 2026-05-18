# Bun Zig→Rust リライト merge — 経緯と影響

- **日付**: 2026-05-14
- **カテゴリ**: Backend / Build Tool
- **ソース**:
  - [The Register: Anthropic's Bun Rust rewrite merged at speed of AI](https://www.theregister.com/devops/2026/05/14/anthropics-bun-rust-rewrite-merged-at-speed-of-ai/5240381)
  - [Hacker News discussion](https://news.ycombinator.com/item?id=48132488)
  - [Bun Releases (oven-sh/bun)](https://github.com/oven-sh/bun/releases)

## 概要

2026-05-14、Bun の中核実装を Zig から Rust にリライトする PR #30412 が main にマージされた。約 96 万行の Zig コードを 6 日間で Rust に移植したもので、コードのほぼ全てを Anthropic の Claude Code エージェントが生成している。Anthropic の Bun 買収後、初の大規模アーキテクチャ変更となる。

注目すべきは、Bun 創業者の Jarred Sumner が「memory safety」を主たる動機として挙げ、パフォーマンスではないと明言している点。Zig は手動メモリ管理ゆえに use-after-free や二重 free 由来のバグ調査に長時間を費やしてきたという。加えて、Zig コミュニティの「AI 生成コード受け入れ拒否」スタンスと、Bun チームの「すでに全てのコードが Claude 生成」という実態の不整合も、移行の現実的な動機となった。

## 主な変更点

### 規模と速度
- マージされた PR #30412 は 6,755 commit、1,000,000 行超の単一ブランチ
- GitHub の安全機構が「異常なサイズ」として警告するレベル
- 6 日間で 960,000 行を移植し、Linux x64 glibc で **テストの 99.8% が成功**
- Anthropic 子会社化後、Bun チームは「数ヶ月前から自分の手でコードを書いていない」と公言

### バイナリ・実行時の改善
- バイナリサイズは **3〜8 MB 縮小**
- 一部のメモリリーク修正を含む
- Rust の所有権モデルにより、コンパイラ支援でメモリ安全性が担保される

### 検証可能性の課題
- 100 万行超の単一マージはレビュー不可能との指摘が複数
- 内部に **約 13,000 個の `unsafe` ブロック** が残存しており、Rust 移行の安全性メリットを限定的にしているとの懸念
- 安定版に取り込まれるのは canary 経由が当面

## 破壊的変更・移行ガイド

ユーザー観点での API 破壊的変更はなく、`bun` の既存ユーザーは透過的に新実装に切り替わる予定。ただし当面は canary チャンネルでの利用が推奨され、安定版反映は段階的になる。

移行を試す場合:
```sh
bun upgrade --canary
```
で Rust ビルドを取得できる。プロダクション利用は時期尚早で、まずは CI やローカル開発で互換性を確認するのが現実的。

## 今後の注目点

- **`unsafe` ブロックの段階的削減**: 13,000 個の `unsafe` を減らせるかが、移行のメリットを実証する鍵
- **Zig フォーク廃止のタイミング**: Bun はこれまで独自パッチを当てた Zig fork を保守してきたが、今後はそのコストから解放される
- **AI 生成コードの大規模 OSS ガバナンス**: 「Claude がほぼ全てのコードを書く OSS」がメインストリームになるか、レビュー・責任・著作権面でどう扱われるかの試金石
- **競合ランタイム（Node.js / Deno）の反応**: Node.js コア / Deno がメモリ安全性をどう打ち出すか、Bun の Rust 移行がプレッシャーになる可能性
- **パフォーマンス測定**: 公式は「メモリ安全性が主目的」だが、Rust 移行後のベンチマーク差分が出始めるのは今後数週間〜数ヶ月
