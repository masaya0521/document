# Tech Updates — 2026-03-28

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 リリース | JavaScript ベースの最終リリース。9つのデフォルト設定変更と多数の非推奨化により、Go ベースの 7.0 への移行を準備 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 2 | Vite | 8.0 リリース | Rolldown（Rust ベースバンドラー）を統合し、esbuild + Rollup の二重構成を廃止。ビルド速度 10〜30 倍向上 | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 3 | Tailwind CSS | 4.2 リリース | 新カラーパレット4種追加、webpack プラグイン (`@tailwindcss/webpack`) 公式提供、`font-features-*` ユーティリティ追加 | [GitHub](https://github.com/tailwindlabs/tailwindcss/releases) |
| 4 | VS Code | 1.112 リリース（3/18） | Copilot エージェントの自律性拡大、MCP サーバーのサンドボックス化（macOS/Linux）、エディタ内ブラウザデバッグ | [リリースノート](https://code.visualstudio.com/updates/v1_112) |
| 5 | ReSharper for VS Code | 正式リリース（3/5） | 1年間のパブリックプレビューを経て GA。C# コード解析・ナビゲーション・リファクタリングを VS Code / Cursor で利用可能に | [JetBrains ブログ](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 6 | Svelte / SvelteKit | 2026年3月アップデート | `createContext` によるプログラム的コンポーネント生成、`{@html}` での TrustedHTML サポート、サーバーサイドエラーバウンダリ | [公式ブログ](https://svelte.dev/blog/whats-new-in-svelte-march-2026) |
| 7 | Rider | 2026.1 RC（3/20） | スタンドアロン .cs ファイルの実行・デバッグ、ASM Viewer、CMake プロジェクトのベータサポート、C++ デバッグ性能最大87倍改善 | [JetBrains ブログ](https://blog.jetbrains.com/dotnet/2026/03/20/rider-2026-1-release-candidate/) |
| 8 | Django | 6.0.3 セキュリティリリース（3/3） | URLField の Unicode 正規化による DoS 脆弱性（CVE-2026-25673）と、マルチスレッド環境でのファイル権限の問題（CVE-2026-25674）を修正 | [Django ブログ](https://www.djangoproject.com/weblog/2026/mar/03/security-releases/) |
| 9 | ReSharper | 2026.1 RC（3/20） | 新しい Monitoring ツールウィンドウでランタイムパフォーマンス監視、コード解析・言語サポートの改善 | [JetBrains ブログ](https://blog.jetbrains.com/dotnet/2026/03/20/resharper-2026-1-release-candidate/) |
| 10 | @tailwindcss/vite | Vite 8 対応（3/12） | `@tailwindcss/vite` の peer dependency に Vite ^8 を追加、テストスイートを Vite 8 対応に更新 | [GitHub PR #19790](https://github.com/tailwindlabs/tailwindcss/pull/19790) |

## Deep Dive

- [TypeScript 6.0 — JavaScript ベース最終リリースと Go 移行への道](./tu-typescript-6-0.md)
- [Vite 8.0 — Rolldown 統合によるアーキテクチャ刷新](./tu-vite-8-0.md)
