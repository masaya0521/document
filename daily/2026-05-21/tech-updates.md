# Tech Updates — 2026-05-21

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Angular | v22 リリース（2026-05-13） | Signal Forms が experimental → stable へ昇格、Zoneless 路線をさらに固め、`debounced()` シグナルや Vitest デフォルトテストランナー、TypeScript 5.9 サポートを追加 | [Angular Blog](https://blog.angular.dev/announcing-angular-v22-feature-overview), [Angular v21 Release Event](https://angular.dev/events/v21) |
| 2 | Node.js | v26.1.0 リリース（2026-05-07） | 実験的な FFI モジュール（`--experimental-ffi`）でダイナミックライブラリと native symbol 呼び出しを実現。`crypto.randomUUIDv7()`、`fs.stat()` の signal サポート、npm 11.13.0 を同梱 | [Node.js Release](https://nodejs.org/en/blog/release/v26.1.0) |
| 3 | React | 19.2.6 / 19.0.6 リリース（2026-05-06） | 19 系のセキュリティ・型強化・パフォーマンス改善を含むメンテナンスリリース。Next.js 16 系の 5 月セキュリティ修正と歩調を合わせた更新 | [React Versions](https://react.dev/versions), [React EOL Tracker](https://eosl.date/eol/product/react/) |
| 4 | Next.js | 16.2.6 LTS リリース（2026-05-07） | Next.js 16 系の LTS 更新。Turbopack 高速化と AI 改善（AGENTS.md・browser log forwarding 等）を含む 16.2 系の安定化パッチ。canary では 16.3 系が進行中 | [Next.js Blog](https://nextjs.org/blog/next-16-1), [Next.js EOL Tracker](https://eosl.date/eol/product/nextjs/) |
| 5 | Python | 3.14.5 リリース（2026-05-10） | 3.14 系のメンテナンスリリース。3.15 ベータ系列と並行して提供。Python 3.14.x はバグ修正と安定化を継続 | [Python Insider Blog](https://blog.python.org/2026/04/python-3150a8-3144-31313/), [Python Status](https://devguide.python.org/versions/) |
| 6 | Svelte / SvelteKit | What's new in Svelte: May 2026 | SvelteKit の remote functions に大量の改善、TypeScript 6.0 サポート追加、Svelte CLI で community add-ons が experimental 公開（`sv@0.1.0`）。`svelte@5.55.0` で TweenOptions / SpringOptions の型エクスポート | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-may-2026) |
| 7 | GitHub Copilot | 5 月の主要アップデート（2026-05-18〜20） | Copilot Chat に semantic issue search、VS Code で auto model selection、Gemini 3.5 Flash の GA、Copilot Spaces API の GA、Copilot cloud agent から review feedback を直接 apply 等、開発者向け機能が連続投入 | [GitHub Changelog](https://github.blog/changelog/2026-05-20-updates-to-available-models-in-copilot-on-web/) |
| 8 | JetBrains AI Assistant | VS Code 向け拡張が public preview | JetBrains の AI Assistant が VS Code 拡張として公開プレビュー開始。Java / Kotlin / JavaScript / Python / C# 対応、コードベース全体を理解した multi-file edit に対応する AI Chat | [Neowin](https://www.neowin.net/news/jetbrains-ai-assistant-lands-on-visual-studio-code-as-an-extension/) |
| 9 | pgBackRest | 共同スポンサーシップで再起動（2026-05-20） | Crunchy Data 売却後、単独メンテナ依存だった PostgreSQL のバックアップツール pgBackRest を、AWS / Percona / Supabase / pgEdge ら複数社が共同で資金支援。プロジェクト存続が確保 | [The Register](https://www.theregister.com/databases/2026/05/20/postgresql-backup-tool-gets-some-backup-of-its-own-after-sole-maintainer-sounds-alarm/) |
| 10 | Google Antigravity | Antigravity 2.0 / Antigravity CLI 発表（2026-05-21, I/O 2026） | サブエージェントによる複雑ワークフロー対応の Antigravity 2.0。CLI もリリースされ、cross-platform terminal sandboxing・credential masking・hardened Git policies を組み込み | [Google Developers Blog](https://developers.googleblog.com/all-the-news-from-the-google-io-2026-developer-keynote/) |

## Deep Dive

- [Angular 22 — Signal-First 時代の確立と Vitest デフォルト化](./tu-angular-22.md)
- [Node.js 26.1.0 — 実験的 FFI モジュールで native ライブラリ呼び出しを解禁](./tu-node-26-1-ffi.md)
