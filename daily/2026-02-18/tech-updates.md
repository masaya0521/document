# Tech Updates — 2026-02-18

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Go | v1.26 リリース | Green Tea GC がデフォルト有効化、cgo オーバーヘッド約30%削減、実験的 SIMD パッケージ追加。`go fix` コマンドが完全刷新され、新しい言語機能への移行を支援する「modernizers」を搭載。言語仕様では `new` の初期値指定やジェネリクスの自己参照型パラメータが追加。 | [Go Blog](https://go.dev/blog/go1.26) |
| 2 | TypeScript | v6.0 Beta | JavaScript ベース最後のリリース。`strict` がデフォルト true、`module` が esnext、`target` が当年 ES バージョンにデフォルト変更。Temporal 型サポート追加。Go ベースの 7.0（5-10倍高速化）への移行準備として `--stableTypeOrdering` フラグを導入。RC は 2/24、正式版は 3/17 予定。 | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/) |
| 3 | Vite | v8.0.0-beta.14 | Rolldown（Rust 製バンドラ）ベースに移行し、esbuild + Rollup の組み合わせを置換。プロダクションビルドが大幅に高速化（SPA で約5倍の報告あり）。Rollup 互換プラグイン API を維持しつつ、Module Federation やモジュールレベル永続キャッシュなどの高度な機能を解放。 | [Vite Blog](https://vite.dev/blog/announcing-vite8-beta) |
| 4 | Kotlin | v2.3.0 リリース | 未使用戻り値チェッカー、明示的バッキングフィールド、Java 25 サポート。Kotlin/Native で Swift export 改善、Kotlin/Wasm で新例外ハンドリングがデフォルト有効。Gradle 9.0 互換、安定した時間追跡 API と改善された UUID 生成。 | [Kotlin Blog](https://blog.jetbrains.com/kotlin/2025/12/kotlin-2-3-0-released/) |
| 5 | Android | 17 Beta 1 | Developer Preview を廃止し Canary トラックに移行、Beta 1 が 2/13 リリース。アダプティブレイアウトの必須化、カメラ・メディア機能の強化、セキュア・バイ・デフォルトアーキテクチャの導入。プラットフォーム安定版は3月、正式版は6月予定。 | [Android Developers Blog](https://android-developers.googleblog.com/2026/02/the-first-beta-of-android-17.html) |
| 6 | Svelte | v5.47.0〜5.49.0 | カスタム `<select>` 要素の CSS/HTML カスタマイズ対応、CSS パーサー（`parseCss`）のエクスポート追加、`ShadowRootInit` サポート。Vercel アダプタでリモート関数呼び出しの observability 改善。エコシステム全体で5件のセキュリティパッチ。 | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-february-2026) |
| 7 | VS Code | v1.110 (Insiders) | チャット会話でのプロンプトキューイング対応（前のタスク処理中に次のプロンプトを送信可能）。モバイルデータ接続時の自動更新延期、スクリーンリーダー向けチャットチップのアクセシビリティ改善。 | [VS Code Updates](https://code.visualstudio.com/updates/v1_110) |
| 8 | Ktor | v3.4.0 リリース | Kotlin 向け非同期 Web フレームワーク。デュプレックスストリーミングサポート追加、リクエストライフサイクルの制御強化、圧縮オプションの拡張。 | [Kotlin Blog](https://blog.jetbrains.com/kotlin/2026/02/kodees-kotlin-roundup-kotlinconf-26-updates-new-releases-and-more/) |
| 9 | Redis Enterprise for K8s | v8.0.10-21 | ARM アーキテクチャのトランスペアレントサポートを追加。Docker Hub 等のコンテナレジストリがノードアーキテクチャに基づいて自動的に適切なイメージを提供。Redis Software 8.0.10-64 対応。 | [Redis Docs](https://redis.io/docs/latest/operate/kubernetes/release-notes/8-0-10-releases/8-0-10-21-feb2026/) |
| 10 | JetBrains Rider | 2026.1 EAP 開始 | 次期メジャーバージョンの Early Access Program が開始。.NET 開発向けの新機能プレビューが利用可能に。ReSharper 2025.3 の追加アップデートも同時リリース。 | [JetBrains Blog](https://blog.jetbrains.com/category/releases/) |

## Deep Dive

- [Go 1.26 — Green Tea GC、SIMD、go fix の大幅刷新](./tu-go-1-26.md)
- [TypeScript 6.0 Beta — JavaScript ベース最後のリリースと Go ベース 7.0 への道](./tu-typescript-6-0-beta.md)
