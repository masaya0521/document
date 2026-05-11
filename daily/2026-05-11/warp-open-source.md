# Warp が OSS 化 — AI エージェント時代のターミナル戦略

- **日付**: 2026-05-11
- **カテゴリ**: Tech
- **ソース**: [Warp Blog](https://www.warp.dev/blog/warp-is-now-open-source) / [The New Stack](https://thenewstack.io/warp-open-source-client/) / [SD Times](https://sdtimes.com/agentic-ai/warps-new-chapter-ushering-in-the-era-of-open-agentic-development/)

## 概要

Warp は 5 月初頭、自社のターミナル / エージェント型開発環境クライアントの全コードを GitHub 上で公開した。リポジトリは [github.com/warpdotdev/warp](https://github.com/warpdotdev/warp)。UI フレームワーク（`warpui_core`、`warpui` クレート）は MIT、その他のコードベースは AGPLv3 でライセンスされている。公開直後から数日で 37,000 スターを超え、GitHub Trending で #2 まで上昇した。

注目すべきは、OpenAI が「creating sponsor」（創設スポンサー）として参加し、新しいエージェント管理ワークフローが GPT モデルで駆動される点である。Warp 自身は OpenAI に出資されているわけではないが、エージェントを介したコード貢献を OpenAI が後援する構図になっている。

## 詳細

### なぜ今 OSS 化したか

Warp は CEO Zach Lloyd によれば、創業から 5 年間「いずれは OSS 化する」前提で動いていたが、毎年議論を重ねた末、これまでは見送ってきた。今年踏み切った最大の理由は **エージェント中心の開発スタイル**が普及したことにある。コードを書く主体が人間からエージェントへ移ると、

- ターミナル / IDE はエージェントの「ホスト」になり、UI よりもプロトコルとオーケストレーションが価値の源泉になる
- エージェントが手元のクライアントを自由に拡張できるよう、コード自体が読める / 改変できる状態であるほうが UX 上有利
- クローズドな AI コーディング製品（Cursor、Cognition、Cloud IDE 系）に対して、OSS を旗印に差別化できる

という条件が揃ったと判断した。

### "Open Agentic Development" モデル

Warp は今回の OSS 化を単なるライセンス変更ではなく、**新しい開発スタイルの提唱**として位置付けている。Warp 内製のクラウド・エージェント・オーケストレーション基盤 **Oz** をベースに、エージェントが実装、人間がレビュー / 方向付けを担当するワークフローを推奨する。コミュニティはエージェント経由で PR を作る前提で参加でき、Warp 側がエージェントの行動を Oz でガードする。

### ライセンス戦略の意味

AGPLv3 はネットワーク経由でのサービス提供時にもソース公開を要求する強コピーレフトで、競合 SaaS による「クローズドな商用フォーク」を許さない。一方で UI 層は MIT にしてコミュニティの組み込みは容易にしてある。「真の OSS にしつつ、商用クローンによる収奪を防ぐ」古典的な戦略を、AI エージェント時代に再適用した格好だ。

## 今後の注目点

- **対抗陣営の動き**: Cursor、Cognition（Devin）、JetBrains AI、Zed などが OSS 化や API 開放に動くか。閉じたままで競争力を維持できるかが試される。
- **Oz / オーケストレーション層のオープン化**: 現状クライアントだけが OSS で、エージェント実行基盤 Oz は SaaS のまま。ここを開けるかどうかが「真の OSS」かのリトマス試験紙になる。
- **OpenAI の関与の深さ**: Anthropic との Claude Code、Google との Gemini CLI に対し、OpenAI 陣営の「公式エージェント開発体験」として Warp を押し出していくのか。
- **既存 SaaS 顧客への影響**: 既存の Warp チーム向け有償プランとの棲み分け。AGPL を嫌う企業向けにデュアルライセンスを導入する可能性。
- **Rust 製ターミナル / TUI エコシステム**: Warp の Rust 実装が OSS 化されたことで、Alacritty・WezTerm・Ghostty といった既存 OSS ターミナルとのコード共有や標準化が進むか。
