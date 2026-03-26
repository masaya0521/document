# Apple Siri のサードパーティAI開放 — iOS 27 の戦略転換

- **日付**: 2026-03-27
- **カテゴリ**: Tech
- **ソース**: [9to5Mac](https://9to5mac.com/2026/03/26/ios-27-apple-will-reportedly-let-claude-and-other-ai-chatbot-apps-integrate-with-siri/)、[Bloomberg](https://www.bloomberg.com/news/articles/2026-03-26/apple-plans-to-open-up-siri-to-rival-ai-assistants-beyond-chatgpt-in-ios-27)、[MacRumors](https://www.macrumors.com/2026/03/26/apple-ios-27-siri-chatbot-integration/)

## 概要

AppleがiOS 27でSiriにサードパーティAIチャットボットとの連携機能を導入する計画が報じられた。これまでのChatGPTとの独占パートナーシップを転換し、Claude（Anthropic）、Gemini（Google）など複数のAIサービスをSiri経由で利用可能にするプラットフォーム戦略への移行を意味する。WWDC 2026（6月8日）での発表が予定されている。

## 詳細

### Extensions システムの仕組み

AppleはSiriに新たな「Extensions」アーキテクチャを導入する。これにより、インストール済みのAIチャットボットアプリが「agents」としてSiriと連携可能になる。

- **設定方法**: ユーザーはSettings > Apple Intelligence & Siriの「Extensions」セクションから利用するAIサービスを選択
- **アプリ配布**: App Store経由でチャットボットアプリをダウンロードし、Extension として有効化
- **動作イメージ**: 現在のChatGPT連携と同様に、Siriが質問を外部AIに転送するフロー

### 独占からプラットフォームへの転換

Apple は当初OpenAIとの独占契約でChatGPTをSiriに統合したが、iOS 27ではこのモデルを根本的に変更する：

- **個別交渉の回避**: 各AI企業との個別契約ではなく、標準化されたExtensionsプラットフォームを提供
- **エコシステムの拡張性**: 新規参入するAIサービスもExtensions対応で即座にSiri連携が可能
- **Apple Intelligenceとの共存**: Apple独自のAI機能は独立して動作し、サードパーティAIはあくまで補完的な位置づけ

### 対応予定のAIサービス

報道で名前が挙がっているサービス：
- **ChatGPT**（OpenAI）— 既存パートナー、引き続き対応
- **Claude**（Anthropic）— 新規対応
- **Gemini**（Google）— 新規対応。なおGoogleとはApple Intelligenceのバックエンド（Private Cloud Compute）でも協力関係

### 対応プラットフォーム

iOS 27、iPadOS 27、macOS 27で同時に提供予定。

## 今後の注目点

- **WWDC 2026（6/8）** でのExtensions APIの技術詳細発表。開発者がどの程度のカスタマイズが可能かが鍵
- **プライバシー設計**: サードパーティAIへのデータ送信時のユーザー同意フローやPrivate Cloud Computeとの関係
- **収益モデル**: AppleがExtensions経由のAIサービス利用に手数料を課すかどうか
- **AI競争への影響**: iPhoneという巨大なディストリビューションチャネルがAIサービス間の競争を加速させる可能性
- **Apple独自AIの位置づけ**: Siri自体のAI能力強化（オンスクリーン認識、クロスアプリ統合）とサードパーティAIの棲み分け
