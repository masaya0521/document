# Tech Updates — 2026-03-11

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 RC リリース | Go ベースの TypeScript 7.0 への橋渡しとなる最後の JS コードベース版。`strict: true` や `target: es2025` のデフォルト化、AMD/UMD/SystemJS の廃止など大規模な破壊的変更を含む | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/) |
| 2 | Rust | 1.94.0 リリース | `array_windows` の安定化、AVX-512 FP16 / AArch64 NEON FP16 intrinsics の安定化、Cargo の `include` 設定キーの安定化、TOML v1.1 対応 | [Rust Blog](https://blog.rust-lang.org/2026/03/05/Rust-1.94.0/) |
| 3 | VS Code | v1.110 リリース | エージェント向け hooks・会話フォーク・メッセージキュー機能を追加。ブラウザ自動操作ツール統合、Copilot CLI 内蔵 | [GitHub Blog](https://github.blog/changelog/2026-03-06-github-copilot-in-visual-studio-code-v1-110-february-release/) |
| 4 | GitHub Copilot | GPT-5.4 対応 | OpenAI GPT-5.4 が Copilot Pro/Business/Enterprise で利用可能に。推論能力とマルチステップタスク対応が向上 | [GitHub Changelog](https://github.blog/changelog/2026-03-05-gpt-5-4-is-generally-available-in-github-copilot/) |
| 5 | Svelte / SvelteKit | 5.53.0 / Kit 2.53.0 | エラーバウンダリのサーバーサイド対応、HTML タグ内コメント対応、Vite 8 サポート開始 | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-march-2026) |
| 6 | C++26 | 最終承認投票フェーズ | 静的リフレクション・コントラクト・std::execution を含む C++26 が 3/23-28 ロンドン会議で最終承認投票へ | [InfoQ](https://www.infoq.com/news/2025/06/cpp-26-feature-complete/) |
| 7 | .NET | 8.0.25 / 9.0.14 セキュリティ更新 | March Patch Tuesday で CVE-2026-26127（DoS）、CVE-2026-26130（ASP.NET Core DoS）、CVE-2026-26131（権限昇格）を修正 | [.NET Blog](https://devblogs.microsoft.com/dotnet/dotnet-and-dotnet-framework-march-2026-servicing-updates/) |
| 8 | pnpm | 11.0.0-alpha.13 | trustPolicy 設定の追加、グローバルインストールの仮想ストア対応、グローバルパッケージの分離インストール | [npm](https://www.npmjs.com/package/pnpm?activeTab=versions) |
| 9 | Vue | 3.6.0-beta.1 | Vapor Mode がフィーチャーパリティ達成（Virtual DOM モードの安定機能と同等）。alien-signals ベースのリアクティビティシステム刷新 | [GitHub Release](https://github.com/vuejs/core/releases/tag/v3.6.0-beta.1) |
| 10 | SvelteKit adapter-netlify | 6.0.0（破壊的変更） | `platform.context` が Netlify Functions 形式に移行、`netlify.toml` でのリダイレクト設定対応 | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-march-2026) |

## Deep Dive

- [TypeScript 6.0 RC — Go ベース TypeScript 7.0 への橋渡し](./tu-typescript-6-rc.md)
