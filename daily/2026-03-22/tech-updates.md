# Tech Updates — 2026-03-22

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Vite | v8.0 リリース | Rolldown を単一の Rust ベースバンドラーとして統合、10-30x 高速ビルドを実現。開発時と本番ビルドの二重構成を解消 | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 2 | Next.js | v16.2 リリース | 開発時起動 87% 高速化、サーバーコンポーネントのレンダリング 25-60% 高速化、Adapters API 安定版昇格 | [公式ブログ](https://nextjs.org/blog/next-16-2) |
| 3 | TypeScript | 6.0 RC リリース | JS コードベース最後のリリース。`strict` がデフォルト `true` に変更、Temporal API 対応、Go ベース TS7 への橋渡し | [DevBlogs](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/) |
| 4 | JDK | 26 GA リリース | HTTP/3 サポート、ポスト量子暗号対応 JAR 署名、AOT キャッシュの GC 非依存化、Applet API 完全削除 | [Oracle](https://www.oracle.com/news/announcement/oracle-releases-java-26-2026-03-17/) |
| 5 | VS Code | 1.112 リリース | 統合ブラウザデバッグ、MCP サーバーサンドボックス化、Copilot CLI 権限管理、エージェント画像対応 | [Releasebot](https://releasebot.io/updates/microsoft/visual-studio-code) |
| 6 | Rust | 1.94.0 リリース | `array_windows` メソッド追加、Cargo が TOML v1.1 対応、AVX-512 FP16 / AArch64 NEON FP16 安定化 | [Rust Blog](https://blog.rust-lang.org/2026/03/05/Rust-1.94.0/) |
| 7 | SvelteKit | 2.53.0 リリース | Vite 8 サポート開始。Svelte 本体も 5.53.0 でサーバーサイドエラー境界対応 | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-march-2026) |
| 8 | Tailwind CSS | v4.2.2 リリース | Vite 8 公式サポート追加、bare value の正規化修正 | [GitHub](https://github.com/tailwindlabs/tailwindcss/releases/tag/v4.2.2) |
| 9 | Go | 1.26.1 リリース | crypto/x509、html/template、net/url、os パッケージのセキュリティ修正 | [Go Release History](https://go.dev/doc/devel/release) |
| 10 | IntelliJ IDEA | 2025.3.4 リリース | Java 26 フルサポート（HTTP/3、パターンマッチングなど10の JEP に対応） | [JetBrains Blog](https://blog.jetbrains.com/idea/2026/03/intellij-idea-2025-3-4/) |

## Deep Dive

- [Vite 8.0 — Rolldown 統合による次世代ビルドツール](./tu-vite-8.md)
- [TypeScript 6.0 RC — JS コードベース最後のリリースと Go ベース TS7 への道](./tu-typescript-6-rc.md)
