# Bun — Zig → Rust 移植検討の波紋

- **日付**: 2026-05-07
- **カテゴリ**: Backend / Runtime
- **ソース**: [The Register (2026-05-05)](https://www.theregister.com/2026/05/05/bun_rust_port/), [Lobste.rs スレッド](https://lobste.rs/s/otxkjw/bun_js_runtime_is_being_vibe_ported_from), [Simon Willison on X](https://x.com/simonw/status/2051476878712840407)

## 概要

JavaScript ランタイムの Bun が、実装言語を Zig から Rust へ移植する可能性を検討していることが明らかになった。きっかけは、Bun のリポジトリに `docs/PORTING.md` が追加され、coding agent（AI コードアシスタント）に移植を支援させる手順が記載されていたこと。発見者の Simon Willison が X に投稿し、技術系コミュニティで一気に広まった。

Bun の作者 Jarred Sumner は「移植への確約はなく、動く形がどう見えるか興味があるだけ」とコメントしており、現時点では公式な移行プロジェクトではなく試行段階に留まる。とはいえ、Anthropic が 2025 年末に Bun を買収し、Claude Code のランタイムとして採用していることを踏まえると、戦略的判断が背景にある可能性が高い。

## 主な変更点

- **`docs/PORTING.md` の公開**: Bun リポジトリに、Zig コードベースを Rust に移植するための手引きが追加された。AI agent が「型情報のマッピング」「メモリ管理規約」「テスト移行」を進めるためのチェックリスト形式
- **コミットメッセージ**: 公式コミットには「rewrite はまだ half-baked（中途半端）」と明記されており、production 移行が近いわけではないことが示されている
- **AI 駆動の移植**: Bun チームは coding agent（おそらく Claude Code）を活用した「vibe-port」と揶揄される手法を採用。コミュニティの一部からは品質懸念の声も

## 背景: なぜ Rust か

Bun は Zig で書かれた数少ない大規模プロジェクトの 1 つで、Zig 採用は競合の Node.js (C++) / Deno (Rust) との差別化要素だった。今回の移植検討の背景には複数の要因がある。

### Zig のエコシステム制約

- Bun チームは Zig を fork し、LLVM の並列コード生成によって macOS/Linux 上で 4 倍のデバッグコンパイル時間短縮を達成
- しかし Zig 本体には **AI 関連の貢献を全面禁止する no-AI ポリシー**（issue / PR / コメントすべて対象）があり、Bun の改善を upstream に戻せない
- Anthropic 傘下の Bun が AI 全面禁止のプロジェクトに依存するのは戦略的に矛盾する

### Rust エコシステムの成熟

- Rust は安全性・並列性・パッケージ管理（cargo）が成熟済み
- 既存の Rust 製ツール（Rolldown, Oxc, Turbopack 等）との統合余地が広がる
- 開発者人口が Zig より圧倒的に多く、コントリビューターを集めやすい

## コミュニティ反応

- 概ね好意的だが、AI 主導の大規模リライトに対する品質懸念は根強い
- Lobste.rs では「vibe-ported」という揶揄混じりの表現で議論が広がる
- 一部ベンチマーク記事（DEV Community）では「現時点では性能差はほぼない」との実測も出ている

## 今後の注目点

- **正式アナウンスのタイミング**: Sumner が「working version を見たい」段階のため、公式ロードマップ化されるかは未定
- **AI 駆動移植の品質検証**: Claude Code 等で生成された Rust コードのレビュー体制と回帰テストが鍵
- **Zig コミュニティへの影響**: Bun は Zig 最大級のユーザー。離脱すれば Zig エコシステム全体に影響が及ぶ
- **Anthropic の戦略開示**: 買収後の Bun の方向性（runtime 単体か、Claude Code 統合か）が言語選択にも影響
