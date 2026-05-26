# Tech Updates — 2026-05-26

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Node.js | v26.0.0 リリース | Temporal API がデフォルト有効化、V8 14.6 へ更新（Map.getOrInsert, Iterator.concat）、Undici 8 搭載。レガシーストリームモジュール削除等の破壊的変更あり | [GitHub](https://github.com/nodejs/node/releases/tag/v26.0.0) |
| 2 | TypeScript | v7.0 Beta | Go への完全移植により最大10倍の高速化を実現。strict デフォルト有効化、ES5 サポート廃止等の破壊的変更。安定版は6-7月予定 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/) |
| 3 | WordPress | 7.0 "Armstrong" リリース | Web Client AI API（OpenAI / Anthropic / Gemini 対応）、Breadcrumbs・Icons ブロック追加、Command Palette（⌘K）搭載の管理画面刷新。リアルタイムコラボレーションは延期 | [公式](https://wordpress.org/news/2026/05/whats-new-for-developers-may-2026/) |
| 4 | PostgreSQL | 18.4 セキュリティアップデート | 11件のセキュリティ脆弱性修正と60件以上のバグ修正。17.10, 16.14, 15.18, 14.23 も同時リリース。tzdata 2026b 更新 | [公式](https://www.postgresql.org/about/news/postgresql-183-179-1613-1517-and-1422-released-3246/) |
| 5 | Tailwind CSS | v4.3 リリース | ファーストパーティのスクロールバースタイリング、論理プロパティユーティリティ追加、zoom・tab-size ユーティリティ、@variant サポート改善 | [GitHub](https://github.com/tailwindlabs/tailwindcss/releases) |
| 6 | Visual Studio 2026 | May Update | AI Copilot Agent Skills パネル、NuGet MCP Server による脆弱性検出・パッケージ更新、システムテーマ連動の自動ダークモード切替 | [公式](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 7 | Google I/O 2026 | 開発者ツール発表 | Android CLI 安定化、Android Studio のクロスプラットフォーム移行ツール、AI Studio での Kotlin/Compose ネイティブアプリ生成、WebMCP 標準提案（Chrome 149 OT） | [Google Blog](https://developers.googleblog.com/all-the-news-from-the-google-io-2026-developer-keynote/) |
| 8 | Spring Boot | 4.1.0-M4（プレリリース） | @AutoConfigureWebServer アノテーション、Jackson read/write 設定プロパティ、LDAP SSL サポート、Spock（Groovy 5）再対応。5月中の GA リリースが見込まれる | [Spring Blog](https://spring.io/blog/2026/03/26/spring-boot-4-1-0-M4-available-now/) |
| 9 | Vue.js | 3.6 Beta（Vapor Mode） | 仮想 DOM を排除しテンプレートを直接 DOM 操作にコンパイル。10万コンポーネントを100msでマウント可能。SolidJS 同等のパフォーマンスを実現。安定版は Q4 2026 見込み | [Vue School](https://vueschool.io/articles/news/vn-talk-evan-you-preview-of-vue-3-6-vapor-mode/) |
| 10 | Ruby | 4.0.5 リリース | 安定版パッチリリース（5月20日） | [公式](https://www.ruby-lang.org/) |

## Deep Dive

- [Node.js 26 — Temporal API デフォルト有効化と主要な破壊的変更](./tu-nodejs-26.md)
- [TypeScript 7.0 Beta — Go 移植による10倍高速化の全貌](./tu-typescript-7-beta.md)
