# Tech Updates — 2026-03-23

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Vite | 8.0 リリース | Rust 製統一バンドラー Rolldown を搭載し、ビルド速度 10-30 倍高速化。DevTools 統合、Wasm SSR 対応も追加 | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 2 | TypeScript | 6.0 RC | Go ベースの TypeScript 7.0 への橋渡しリリース。strict: true デフォルト化、ES5/AMD/UMD 削除等の破壊的変更多数 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/) |
| 3 | Next.js | 16.2 リリース | next dev 起動 約400% 高速化、レンダリング 約50% 高速化。Turbopack 200 以上のバグ修正 | [公式ブログ](https://nextjs.org/blog/next-16-2) |
| 4 | Java | JDK 26 GA (3/17) | HTTP/3 サポート (JEP 517)、PEM エンコーディング API、G1 GC 改善、Applet API 削除など 10 JEP | [Oracle](https://blogs.oracle.com/java/the-arrival-of-java-26) |
| 5 | Rust | 1.94.0 (3/5) | array_windows メソッド追加など安定化。次期 1.95.0 beta は 4/16 予定 | [Rust Blog](https://blog.rust-lang.org/2026/03/05/Rust-1.94.0/) |
| 6 | Go | 1.26.1 / 1.25.8 (3/5) | crypto/x509、html/template、net/url、os パッケージのセキュリティ修正 | [Go Release History](https://go.dev/doc/devel/release) |
| 7 | JetBrains ReSharper | VS Code / Cursor 対応版 正式リリース (3/5) | 1 年の Public Preview を経て正式版に。C# コード解析・リファクタリングを VS Code で利用可能。非商用無料 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 8 | GitHub Actions | Late March 2026 アップデート (3/19) | スケジュールワークフローの IANA タイムゾーン指定、deployment: false による環境利用が可能に | [GitHub Changelog](https://github.blog/changelog/2026-03-19-github-actions-late-march-2026-updates/) |
| 9 | Tailwind CSS | 4.2.2 (3/20 頃) | Vite 8 対応を含むバグ修正・改善リリース | [npm](https://www.npmjs.com/package/@tailwindcss/vite) |
| 10 | Visual Studio | 2026 March アップデート (3/10) | JSON エディタの JSON Schema 新仕様対応、Debugger Agent ワークフロー、C++ Copilot Agent Mode デフォルト有効化 | [Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |

## Deep Dive

- [Vite 8.0 — Rolldown 統合による統一バンドラー時代の到来](./tu-vite-8.md)
- [TypeScript 6.0 RC — Go ベース TypeScript 7.0 への橋渡し](./tu-typescript-6-rc.md)
