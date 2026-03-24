# Tech Updates — 2026-03-25

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | v6.0 リリース | JS ベース最終版。strict デフォルト true、target デフォルト ES2025、Temporal API 型サポート。Go ベースの v7.0 への橋渡し | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 2 | Vite | v8.0 リリース | Rolldown（Rust 製バンドラー）統合により 10-30x 高速化。esbuild/Rollup の二重構成を廃止 | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 3 | Astro | v6.0 リリース | Fonts API、CSP API、Live Content Collections。Vite Environment API による開発サーバー刷新、実験的 Rust コンパイラ | [公式ブログ](https://astro.build/blog/astro-6/) |
| 4 | Laravel | v13 リリース | 破壊的変更ゼロ。AI SDK が正式版に昇格、Passkey 認証、ベクトル検索、JSON:API リソース | [Laravel News](https://laravel-news.com/laravel-13) |
| 5 | VS Code | v1.112 リリース | 統合ブラウザデバッグ、Copilot CLI パーミッション、MCP サーバーサンドボックス。週次リリースに移行 | [公式](https://code.visualstudio.com/updates/v1_112) |
| 6 | Ruby on Rails | v7.2.3.1 / v8.0.4.1 / v8.1.2.1 セキュリティパッチ | 5件以上の CVE（XSS、ReDoS、DoS、Path Traversal）を修正 | [Rails Discussions](https://discuss.rubyonrails.org/t/cve-2026-33169-possible-redos-vulnerability-in-number-to-delimited-in-active-support/90911) |
| 7 | GitHub Dependabot | pre-commit フック対応 | .pre-commit-config.yaml の依存を自動更新。グループ化更新にも対応 | [GitHub Changelog](https://github.blog/changelog/2026-03-10-dependabot-now-supports-pre-commit-hooks/) |
| 8 | JetBrains ReSharper | VS Code / Cursor 拡張正式リリース | C# コード分析・リファクタリングを VS Code / Cursor / Antigravity で利用可能に | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 9 | Deno | v2.7.x パッチリリース (v2.7.2〜v2.7.7) | Temporal API 安定化、Windows ARM サポート、npm overrides 対応。3月中に6回のパッチリリース | [GitHub Releases](https://github.com/denoland/deno/releases) |
| 10 | ReSharper | 2026.1 RC | .NET 開発の高速化・予測性向上。コード分析と言語サポートの改善 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/20/resharper-2026-1-release-candidate/) |

## Deep Dive

- [TypeScript 6.0 — JS ベース最終リリースと Go ベース v7.0 への移行準備](./tu-typescript-6-0.md)
- [Vite 8.0 — Rolldown 統合による Rust ベースビルドツールチェーンへの転換](./tu-vite-8-0.md)
