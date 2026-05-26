# KotlinConf 2026 — Kotlin 2.4 プレビュー・VS Code Alpha・Exposed 1.0

- **日付**: 2026-05-20〜22（ミュンヘン開催）
- **カテゴリ**: Language / Dev Tool / Backend
- **ソース**: [KotlinConf 2026 Keynote Highlights](https://blog.jetbrains.com/kotlin/2026/05/kotlinconf26-keynote-highlights/), [Kotlin for VS Code Alpha](https://blog.jetbrains.com/kotlin/2026/05/official-kotlin-support-for-visual-studio-code-is-now-available-in-alpha/)

## 概要

KotlinConf 2026 が5月20〜22日にミュンヘンで開催され、言語機能・AI ツール・バックエンド開発・マルチプラットフォームの各領域で多数の発表が行われた。Kotlin 2.4.0 のプレビュー、公式 VS Code 拡張の Alpha リリース、Exposed 1.0 安定版、AI エージェントフレームワーク Koog 1.0 が主要なハイライト。

## 主な発表内容

### Kotlin 2.4.0 プレビュー

安全性と利便性を核心原則として強化する次期バージョン。

**安定化される機能:**
- **コンテキストパラメータ** — API をより表現力豊かにし、コアロジックに集中できる設計を実現
- **明示的バッキングフィールド** — バッキングプロパティの定型コードを削減

**実験的機能:**
- **マルチフィールド値クラス** — コンパイラが `equals()` / `hashCode()` を自動生成。名前ベースの分解代入で安全性向上

**標準ライブラリのセキュリティポリシー:**
- Kotlin 2.4 より **18ヶ月のセキュリティサポートポリシー** を導入。アクティブなサポートウィンドウ内の全リリースラインにセキュリティ修正をバックポート

### Kotlin for VS Code — Alpha リリース

公式の Kotlin 拡張機能が Visual Studio Marketplace で利用可能に。

**技術基盤:**
- IntelliJ IDEA のコード解析インフラと Kotlin プラグイン実装をベースにした **Kotlin Language Server** を採用
- VS Code での Kotlin 機能が IntelliJ IDEA と同じ基盤で動作

**Alpha で提供される機能:**
- コード補完
- 診断（エラー・警告表示）
- ナビゲーション（定義へのジャンプ等）
- クイックフィックス
- フォーマット
- プロジェクトインポート

**位置付け:** IntelliJ IDEA / Android Studio が「最も完全な Kotlin 開発環境」であることに変わりはなく、VS Code 版は補完的ツールとしての位置付け。

### AI 開発ツール

- **Junie** — JetBrains 製コーディングエージェント。IDE に深く統合され、複数の LLM プロバイダーに対応。Android 専用サポートあり
- **Agent Client Protocol (ACP)** — IDE とコーディングエージェント間の通信方法を規定するオープン標準。JetBrains が共同策定
- **Anthropic 連携** — Anthropic の JVM SDK は Kotlin 実装。Claude が IntelliJ IDEA / Android Studio に統合。Kotlin SWE-bench で Claude Code (Opus 4.7) が 86.4% の解決率を達成

### バックエンド開発

- **Exposed 1.0** — Kotlin 製 ORM の安定版リリース。AI 類似性検索向けベクタ型対応と Gradle プラグインを搭載
- **Koog 1.0** — AI エージェントフレームワーク。型安全なワークフロー DSL、長期実行エージェント向けの永続性・復旧機能を提供。Mercedes-Benz が車両保守支援エージェント構築に採用
- **Ktor / kotlinx-rpc** — Koog との統合で AI パワードサービスの構築が可能に

### マルチプラットフォーム

- Kotlin Multiplatform (KMP) 採用企業が過去1年で **倍増**。PayPal、Booking.com、Sony 等が本番運用
- **Compose Multiplatform** — モバイル・デスクトップは完全安定版、Web は Beta
- **Swift Export** — Kotlin 2.4 で Alpha に昇格。iOS 開発との相互運用性が向上
- **SPM import** — Swift Package Manager 経由の依存関係追加に対応
- **Kotlin/Native** — ビルド時間 25% 高速化、RAM 使用量 50% 削減
- コミュニティライブラリは klibs.io に **3,500 以上** 掲載

## 今後の注目点

- Kotlin 2.4.0 の正式リリース時期（2026年後半の見込み）
- Kotlin for VS Code の Beta 昇格と機能追加（デバッグ、リファクタリング等）
- Koog / Exposed の本番採用事例の拡大
- ACP のエコシステム拡大と他 IDE への波及
