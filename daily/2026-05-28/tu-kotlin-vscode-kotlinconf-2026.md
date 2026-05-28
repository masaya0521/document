# Kotlin VS Code Extension Alpha — KotlinConf 2026 ハイライト

- **日付**: 2026-05-28
- **カテゴリ**: Dev Tool / プログラミング言語
- **ソース**: [JetBrains Blog — VS Code Extension](https://blog.jetbrains.com/kotlin/2026/05/official-kotlin-support-for-visual-studio-code-is-now-available-in-alpha/), [KotlinConf'26 Keynote Highlights](https://blog.jetbrains.com/kotlin/2026/05/kotlinconf26-keynote-highlights/), [Kotlin Language Server (GitHub)](https://github.com/Kotlin/kotlin-lsp)

## 概要

KotlinConf 2026（5月20-22日、ミュンヘン）で、JetBrains は公式 Kotlin VS Code Extension のアルファ版をリリースした。IntelliJ IDEA のコードインサイト基盤をそのまま活用した Kotlin Language Server を経由することで、VS Code や Cursor などの LSP 対応エディタで IntelliJ 品質の Kotlin サポートを利用できるようになる。同キーノートでは Kotlin 2.4.0 プレビュー、Koog 1.0、Kotlin Toolchain なども発表された。

## Kotlin VS Code Extension Alpha

### 提供機能

- コード補完（IntelliJ エンジンベース）
- 診断（エラー・警告のリアルタイム表示）
- ナビゲーション（定義へのジャンプ、参照検索）
- クイックフィックス
- コードフォーマット
- プロジェクトインポート（Gradle / Maven）

### 技術基盤

```
VS Code ←→ Kotlin Language Server ←→ IntelliJ IDEA コードインサイト基盤
                                        └── Kotlin プラグイン実装
```

LSP（Language Server Protocol）を介して通信するため、VS Code だけでなく Cursor や Google Antigravity など LSP 対応エディタ全般で利用可能。

### インストール

Visual Studio Marketplace で「Kotlin by JetBrains」を検索してインストール。

### 現時点の制限事項

- アルファ版のため安定性・パフォーマンスは改善途上
- IntelliJ IDEA / Android Studio の全機能を網羅しているわけではない
- フィードバックは [GitHub リポジトリ](https://github.com/Kotlin/kotlin-lsp) で受付

## KotlinConf 2026 — その他の主要発表

### Kotlin 2.4.0 プレビュー

| 機能 | 状態 | 概要 |
|------|------|------|
| コンテキストパラメータ | 安定化予定 | 暗黙的なコンテキスト注入で API をシンプルに |
| 明示的バッキングフィールド | 安定化予定 | バッキングプロパティのボイラープレート削減 |
| マルチフィールド値クラス | 実験的 | 複数フィールドを持つ value class |
| 18ヶ月セキュリティサポート | 2.4 から | 標準ライブラリのセキュリティ修正バックポート |

### Kotlin Toolchain

ビルド・実行・テスト・フォーマット・ドキュメント生成・エージェント統合を統一する新しいエコシステムエントリーポイント。

### AI・エージェント関連

- **Junie**: JetBrains のコーディングエージェント。複数 LLM プロバイダー対応、Android 専用サポート搭載
- **JetBrains Air**: 複数エージェント向けの開発環境
- **Anthropic 連携**: Claude が IntelliJ IDEA / Android Studio にネイティブ統合。Kotlin SWE-bench で Claude Code が 86.4% の解決率を達成
- **Koog 1.0**: Kotlin AI エージェントフレームワークの安定版リリース
- **Agent Client Protocol (ACP)**: IDE とコーディングエージェント間の通信オープン標準（JetBrains 共同策定）

### Kotlin Multiplatform (KMP)

- トップアプリでの KMP 採用が1年で倍増（PayPal, Booking.com, Sony, Duolingo 等）
- Compose Multiplatform がモバイル・デスクトップで本番対応、Web 版がベータ到達
- klibs.io に 3,500 以上のコミュニティライブラリが登録

## 今後の注目点

- Kotlin VS Code Extension のベータ昇格時期と機能拡充ロードマップ
- Kotlin Toolchain の GA リリースと既存ビルドツールとの統合
- ACP（Agent Client Protocol）の標準化とエディタ間の普及
- Koog フレームワークを使った Kotlin エージェント開発の事例
- Compose for Web のベータ → 安定版への移行
