# Tech Updates — 2026-04-13

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | v6.0 リリース | JavaScript ベース最後のバージョン。strict デフォルト化、ES5 ターゲット廃止。Go リライト（Project Corsa）で 10 倍高速化へ | [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/03/23/typescript-6-0-ships-as-final-javascript-based-release-clears-path-for-go-native-7-0.aspx) |
| 2 | Vite | v8.0 リリース | Rolldown（Rust 製統一バンドラー）採用で 10-30 倍高速ビルド。DevTools 統合、Wasm SSR 対応 | [Vite Blog](https://vite.dev/blog/announcing-vite8) |
| 3 | Next.js | v16.2 リリース | dev 起動 87% 高速化、RSC レンダリング最大 350% 向上、Adapter API 安定化、AI Agent DevTools（実験的） | [Next.js Blog](https://nextjs.org/blog/next-16-2) |
| 4 | VS Code | v1.115 リリース | VS Code Agents コンパニオンアプリ、統合ブラウザ改善、ターミナルツール強化、ミニマップにテストカバレッジ表示 | [VS Code Updates](https://code.visualstudio.com/updates/v1_115) |
| 5 | Angular | v21（zoneless デフォルト化） | zone.js を削除しデフォルトで zoneless に。Signal Forms（実験的）、Vitest が標準テストランナーに | [Angular Blog](https://blog.angular.dev/announcing-angular-v21-57946c34f14b) |
| 6 | Tailwind CSS | v4.2 リリース | Webpack プラグイン追加、新カラーパレット 4 種（mauve, olive, mist, taupe）、論理プロパティユーティリティ、リコンパイル 3.8 倍高速化 | [InfoQ](https://www.infoq.com/news/2026/04/tailwind-css-4-2-webpack/) |
| 7 | GitHub Copilot in VS Code | 3 月リリースまとめ | Autopilot（完全自律エージェントセッション）パブリックプレビュー、Sandbox MCP サーバー、#codebase セマンティック検索改善 | [GitHub Blog](https://github.blog/changelog/2026-04-08-github-copilot-in-visual-studio-code-march-releases/) |
| 8 | PostgreSQL 19 | フィーチャーフリーズ（4/8） | 2026 年 9 月リリース予定。パーティション分割・マージの改善等がコミット済み。ベータは 5 月開始予定 | [VersionLog](https://versionlog.com/blog/postgresql-19-whats-coming-september-2026/) |
| 9 | FastAPI | SSE サポート追加 | Server Sent Events 対応、ストリーミング JSON Lines / バイナリデータの yield サポート、strict_content_type チェックのデフォルト化 | [GitHub Releases](https://github.com/fastapi/fastapi/releases) |
| 10 | Vue | v3.6 Vapor Mode | コンパイル時最適化による極限的なマウント速度を実現するデモ公開。Vue 4 のアイランドアーキテクチャへの布石 | [Vue.js](https://vuejs.org/) |

## Deep Dive

- [Vite 8.0 — Rolldown による統一バンドラー革命](./tu-vite-8-rolldown.md)
- [TypeScript 6.0 — JavaScript 時代の終わりと Go リライトへの道](./tu-typescript-6-go-rewrite.md)
