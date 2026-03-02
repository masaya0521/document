# Tech Updates — 2026-03-02

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Go | v1.26 リリース | Green Tea GC がデフォルト有効化（GC オーバーヘッド 10〜40% 削減）、`new` 関数の構文拡張、ジェネリック型の自己参照が可能に、`go fix` の全面刷新（24 個のモダナイザー搭載） | [公式ブログ](https://go.dev/blog/go1.26) |
| 2 | TypeScript | v6.0 Beta リリース | JS ベースコンパイラ最後のリリース。strict デフォルト化、ES2025 ターゲット、Temporal API 型、subpath imports 対応。ES5・AMD/UMD 等を非推奨化し TS 7.0（Go リライト）への移行を準備 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/) |
| 3 | Rust | v1.93.0 / v1.93.1 リリース | musl 1.2.5 への更新（DNS リゾルバ改善）、`asm!` ブロック内 `cfg` 対応、グローバルアロケータ改善、23 個の API 安定化。1.93.1 はセキュリティ修正 | [公式ブログ](https://blog.rust-lang.org/2026/01/22/Rust-1.93.0/) |
| 4 | Python | v3.14.3 メンテナンスリリース | 299 件のバグ修正・ビルド改善・ドキュメント変更を含む 3.14 系 3 回目のメンテナンスリリース | [Python.org](https://www.python.org/downloads/release/python-3143/) |
| 5 | VS Code | February 2026 (v1.110) | チャットプロンプトのキューイング対応、コンテキストウィンドウ使用量の可視化・圧縮機能、プライベート GitHub リポジトリからのエージェントプラグインインストール対応 | [リリースノート](https://code.visualstudio.com/updates/v1_110) |
| 6 | IntelliJ IDEA | 2026.1 EAP 1〜3 公開 | 次期メジャーバージョン 2026.1 の Early Access Program が進行中。EAP 3 まで公開済み | [JetBrains](https://youtrack.jetbrains.com/articles/IDEA-A-2100662619/IntelliJ-IDEA-2026.1-EAP-3-261.20362.25-build-Release-Notes) |
| 7 | Redis | v8.6.1 セキュリティアップデート | セキュリティパッチ適用。起動時に Transparent Huge Pages (THP) を自動無効化し、レイテンシスパイクとメモリフラグメンテーションを防止 | [Changelog](https://www.clever.cloud/developers/changelog/2026/02-25-redis-8.6.1) |
| 8 | Tailwind CSS | v4.2.1 リリース | @tailwindcss/vite で外部ファイル変更時のフルリロード修正、Oxide スキャナの大規模プロジェクトでのパフォーマンス向上、Astro v5 でのインポートエイリアスクラッシュ修正 | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases) |
| 9 | FastAPI | Starlette 1.0 対応 | Starlette 1.0.0+ のサポートを追加。fastapi-slim パッケージを廃止し `fastapi[standard]` に統一 | [GitHub Releases](https://github.com/fastapi/fastapi/releases) |
| 10 | Rails | v8.1.2 メンテナンスリリース | Rails 8.1 系のバグ修正リリース。Rails 8.0 のバグ修正サポートは 2026-05-07 まで延長 | [公式サイト](https://rubyonrails.org/2026/1/22/rails-version-8-1-2-has-been-released) |

## Deep Dive

- [Go 1.26 — Green Tea GC と主要な新機能](./tu-go-1-26.md)
- [TypeScript 6.0 Beta — Go リライトへの移行準備](./tu-typescript-6-0-beta.md)
