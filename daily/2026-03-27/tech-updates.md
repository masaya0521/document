# Tech Updates — 2026-03-27

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Vite | v8.0 リリース | Rust 製バンドラー Rolldown を統一採用。ビルド速度 10-30x 向上、Linear では 46s→6s に短縮。Vite 2 以来最大のアーキテクチャ変更 | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 2 | Next.js | v16.2 リリース | dev 起動が 16.1 比で約 87% 高速化、Server Components レンダリングが 25-60% 改善。Server Fast Refresh、Agent DevTools（実験的）を追加 | [公式ブログ](https://nextjs.org/blog/next-16-2) |
| 3 | Tailwind CSS | v4.2.2 リリース | 新カラーパレット4種追加（mauve, olive, mist, taupe）、公式 webpack プラグイン、論理プロパティユーティリティ、Vite 8 対応 | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases) |
| 4 | WebStorm | 2026.1 リリース | サービスベース TypeScript エンジンをデフォルト化。Claude Agent・Codex 等の AI エージェント対応、Angular 21.x / Vue / Svelte テンプレート改善 | [JetBrains ブログ](https://blog.jetbrains.com/webstorm/2026/03/webstorm-2026-1/) |
| 5 | ReSharper for VS Code | 正式リリース | 1年間のパブリックプレビューを経て VS Code / Cursor 向け ReSharper が GA。C# コード分析・リファクタリング対応。非商用は無料 | [JetBrains ブログ](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 6 | WordPress | 7.0 RC1 リリース | Real Time Collaboration、クライアントサイド画像最適化等を含むメジャーバージョン RC。正式リリースは 4/9 予定 | [WordPress News](https://wordpress.org/news/2026/03/wordpress-7-0-release-candidate-1/) |
| 7 | Rider | 2026.1 RC リリース | ファイルベース C# プログラム対応、MAUI 開発体験改善（Windows）、混合モードデバッグ、CMake プロジェクト早期サポート | [JetBrains ブログ](https://blog.jetbrains.com/dotnet/2026/03/20/rider-2026-1-release-candidate/) |
| 8 | @vitejs/plugin-react | v6 リリース | Oxc ベースの React Refresh 変換を採用し、Babel 依存を完全に除去。Vite 8 と同時リリース | [GitHub Releases](https://github.com/vitejs/vite/releases) |
| 9 | GitHub CodeQL | v2.25.0 バンドル更新 | 増分解析の改善、TRAP キャッシュ無効化による Actions キャッシュ使用量削減。C/C++ 解析の増分解析ロールアウト進行中 | [GitHub Changelog](https://github.blog/changelog/) |
| 10 | Slack CLI | v3.15.0 リリース | プロジェクトディレクトリ名の kebab-case 正規化、Bolt JS/Python でローカル manifest.json をデフォルト化 | [Slack Dev Docs](https://docs.slack.dev/changelog/2026/03/19/slack-cli/) |

## Deep Dive

- [Vite 8.0 — Rolldown による統一バンドラーアーキテクチャ](./tu-vite-8.md)
- [Next.js 16.2 — 開発体験の大幅高速化と Agent DevTools](./tu-nextjs-16-2.md)
