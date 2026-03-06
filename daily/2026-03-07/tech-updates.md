# Tech Updates — 2026-03-07

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Rust | v1.94.0 リリース | array_windows によるスライスイテレーション、AVX-512 FP16 intrinsics の安定化、Cargo の TOML v1.1 パース対応、17 の API 安定化 | [Rust Blog](https://blog.rust-lang.org/2026/03/05/Rust-1.94.0/) |
| 2 | TypeScript | v6.0 RC リリース | JavaScript ベース最後のリリース。技術的負債の解消と標準化に注力し、Go ベースの TypeScript 7.0 への移行を準備 | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/) |
| 3 | Go | v1.26.1 リリース | セキュリティ修正とバグ修正。Go 1.26 本体は Green Tea GC のデフォルト有効化、cgo オーバーヘッド約30%削減、ジェネリック型の自己参照サポート等 | [Go Blog](https://go.dev/blog/go1.26) |
| 4 | Deno | v2.7.4 パッチリリース | Temporal API の安定化、Windows ARM 公式サポート、npm overrides 対応。3/3〜3/5 に連続パッチリリース (2.7.2〜2.7.4) | [Deno Blog](https://deno.com/blog/v2.7) |
| 5 | JetBrains ReSharper | VS Code / Cursor 向け正式リリース | 1年間のパブリックプレビューを経て、ReSharper の C# コード解析・リファクタリング機能が VS Code、Cursor、その他互換エディタで利用可能に。Open VSX Registry にも登録 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 6 | Astro | v6 安定版リリース間近 | ベータ9回を経て安定版が数週間以内にリリース予定。リデザインされた開発サーバー、レンダリング性能改善、CSP・フォント・ライブコンテンツコレクションの組み込み API | [Astro Blog](https://astro.build/blog/astro-6-beta/) |
| 7 | Slack CLI | v3.14.0 リリース | `slack create` コマンドでカスタムアプリ名のプロンプト表示、Bolt Python プロジェクトでの仮想環境 (.venv) 自動作成・有効化サポート | [Slack Dev Docs](https://docs.slack.dev/changelog/2026/03/05/slack-cli/) |
| 8 | Redis | v8.6.1 セキュリティアップデート | バグ修正とセキュリティパッチ。Transparent Huge Pages (THP) をスタートアップ時に無効化し、レイテンシスパイクとメモリフラグメンテーションを防止 | [Clever Cloud Changelog](https://www.clever.cloud/developers/changelog/2026/02-25-redis-8.6.1/) |
| 9 | Django | v6.0.2 / v5.2.11 セキュリティリリース | 6件のセキュリティ問題を修正。Django 6.0 系、5.2 系、4.2 系の3バージョン同時リリース | [Django News](https://www.djangoproject.com/weblog/2026/) |
| 10 | Bun | v1.3 メジャーアップデート | ゼロコンフィグのフロントエンド開発（HMR、React Fast Refresh 内蔵）、統一データベース API、HTML ファイルの直接実行と自動トランスパイル | [InfoQ](https://www.infoq.com/news/2026/01/bun-v3-1-release/) |

## Deep Dive

- [Rust 1.94.0 — array_windows と AVX-512 FP16](./tu-rust-1-94.md)
- [TypeScript 6.0 RC — JavaScript ベース最後のリリースと Go 移行への道](./tu-typescript-6-rc.md)
