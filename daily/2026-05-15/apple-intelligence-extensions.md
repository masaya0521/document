# Apple Intelligence "Extensions"：Apple が iOS 27 で外部 AI を解禁する戦略的意義

- **日付**: 2026-05-15
- **カテゴリ**: Tech
- **ソース**:
  - [9to5Mac](https://9to5mac.com/2026/05/05/ios-27-will-let-you-choose-between-gemini-claude-and-more-for-ai-features-report/)
  - [The Apple Post](https://www.theapplepost.com/2026/05/09/70705/ios-27-could-let-users-replace-chatgpt-with-gemini-or-claude-for-apple-intelligence/)
  - [AppleMagazine — Siri Extensions Turn Developers Into Apple's AI Battleground](https://applemagazine.com/siri-extensions-2026/)

## 概要

Apple は今秋の iOS 27 / iPadOS 27 / macOS 27 で、Apple Intelligence のバックエンドを Google Gemini や Anthropic Claude といったサードパーティモデルに切り替えられる新機能 "Extensions" を導入する。Siri、Writing Tools、Image Playground といった既存の AI 機能は、ユーザーが Settings から選んだ任意のモデルプロバイダーで動作するようになる。発表は WWDC 2026（6/8 開幕）で予定されている。

これは 2024 年に始まった「ChatGPT 連携」の発展形ではなく、Apple Intelligence の拡張点を OS API として公開する根本的なアーキテクチャ変更である。Apple 自社モデル中心という従来方針からの大きな転換となる。

## 詳細

### Extensions とは何か

Bloomberg ほかの報道によれば、Extensions は「インストール済みアプリから生成 AI 機能をオンデマンドで呼び出せる」プラットフォーム拡張機能群と位置付けられている。具体的には:

- Siri の応答生成エンジンを Gemini / Claude 等に切り替え可能
- Writing Tools（要約・推敲・トーン変換）も外部モデルが処理
- Image Playground の画像生成も外部モデル選択可
- 選択した外部モデルに応じてカスタム音声を Siri に割り当て可能

ユーザーは設定アプリから機能ごと（Siri は Claude、Writing Tools は Gemini など）に異なるプロバイダーを選択できる設計。Apple が内部テストしている統合は少なくとも Google・Anthropic の 2 社で、ChatGPT も既に統合済みのため、初期の選択肢は 3 社が中心になる見通し。

### なぜ今、Apple は方針を変えたのか

3 つの背景が重なっている:

1. **Apple Intelligence の評判の伸び悩み**
   2024-2025 年に投入した Apple 自社のオンデバイス/Private Cloud Compute モデルは、機能性とユーザー満足度の両面で Gemini / Claude / GPT に劣ると評価されてきた。フロンティアモデル開発で他社と並走するコストとリスクを Apple が引き受け続けるより、プラットフォーマーとして "誰の AI を載せるか" を選ばせる側に回る方が合理的という判断。

2. **規制圧力（DMA・MSCA）**
   EU の DMA、日本のモバイルソフトウェア競争促進法（MSCA）など、垂直統合への規制が強まっており、自社モデル独占よりオープンなインターフェースを準備しておく方がリスクが低い。事実、Apple は 5 月時点で iOS 26.2 から日本向けに代替アプリストアを許可する変更も発表している。

3. **エンタープライズとプライバシー要件への対応**
   企業ユーザーや高度なプライバシー要件を持つ層は、Apple のクラウド AI ではなく、契約済みの Anthropic や Google モデル、あるいはオンプレ LLM を使いたいケースが多い。Extensions API はそうした選択肢の受け皿になる。

### 開発者・モデルプロバイダーへの影響

- **Anthropic**: Claude が Apple Intelligence のバックエンド候補に並ぶことで、エンドユーザー接点が一気に拡大する。Anthropic-Akamai の 18 億ドルコンピューティング契約と合わせて、推論需要急増への布石が見える。
- **Google**: Gemini が iPhone の Siri バックエンドになる可能性は、Android との差別化要因（Gemini Intelligence on Android）と矛盾しないかが論点。
- **OpenAI**: 既存の ChatGPT 統合が他社並みに「one of them」になることで、独占的優位は失う。
- **アプリ開発者**: AppleMagazine が指摘するように、Siri Extensions は開発者にとって「自分のアプリの AI 機能を Siri 経由で呼び出せる」新しい配信チャネルになる。

## 今後の注目点

- WWDC 2026（6/8）での正式発表と API 仕様の公開タイミング
- 課金モデル：Apple がモデルプロバイダーから手数料を取るか、Apple Intelligence の有償化と連動するか
- プライバシー：外部モデルへのデータ送信に対する Private Cloud Compute 相当の保証が用意されるか
- 中国市場向けの実装（Apple は中国で別の AI パートナー戦略を取っている）
- Apple 自社モデルの位置付け：完全に内製を縮小するのか、特定機能（オンデバイス処理）に特化するのか
