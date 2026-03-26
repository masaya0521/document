# Tech Updates — 2026-03-26

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 リリース (3/23) | JS ベース最後のリリース。`strict: true` デフォルト化、`target: es2025`、Temporal API 型サポート、多数の非推奨化で Go ネイティブ 7.0 への移行を準備 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 2 | Vite | 8.0 リリース (3/12) | Rolldown（Rust ベース）を統一バンドラーとして採用。esbuild + Rollup の二重構造を解消し、10〜30 倍高速なビルドを実現。統合 Devtools、Wasm SSR サポートも追加 | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 3 | Next.js | 16.2 リリース | dev サーバー起動が 16.1 比約 87% 高速化、レンダリング約 50% 高速化。Server Fast Refresh、AI Agent DevTools（実験的）、AGENTS.md デフォルト生成など | [公式ブログ](https://nextjs.org/blog/next-16-2) |
| 4 | Java | 26 リリース (3/17) | 10 の JEP を含むリリース。AOT キャッシュの全 GC 対応、HPKE 暗号化、ポスト量子対応 JAR 署名、Unicode 17.0 / CLDR v48 対応、Applet API 削除 | [Oracle](https://www.oracle.com/news/announcement/oracle-releases-java-26-2026-03-17/) |
| 5 | Rust | 1.94.0 リリース (3/5) | `array_windows` でスライスの固定長ウィンドウイテレーション、x86 AVX-512 FP16 intrinsics 安定化、Cargo の TOML 1.1 サポート、数学定数（EULER_GAMMA, GOLDEN_RATIO）追加 | [公式ブログ](https://blog.rust-lang.org/2026/03/05/Rust-1.94.0/) |
| 6 | Go | 1.26 リリース (2/10) | Green Tea GC がデフォルト有効化（短命オブジェクトで 10〜40% 効率向上）、cgo オーバーヘッド約 30% 削減、自己参照ジェネリクス型、pprof デフォルト Flame Graph 表示 | [公式ブログ](https://go.dev/blog/go1.26) |
| 7 | VS Code | 1.112 リリース (3/18) | エディタ内ブラウザデバッグ統合、MCP サーバーサンドボックス（macOS/Linux）、Copilot CLI の 3 段階権限モデル（Default/Bypass/Autopilot）、Agent 画像サポート | [リリースノート](https://code.visualstudio.com/updates/v1_112) |
| 8 | IntelliJ IDEA | 2026.1 リリース | ACP レジストリで AI エージェント（Codex, Cursor 等）をワンクリック導入、DB アクセス開放、Java 26 / Kotlin JPA サポート強化、Spring ランタイムインサイト、1,000+ バグ修正 | [公式ブログ](https://blog.jetbrains.com/idea/2026/03/intellij-idea-2026-1/) |
| 9 | ReSharper | VS Code 正式版リリース (3/5) | 1 年間のパブリックプレビューを経て GA。C# コード分析・リファクタリング・フォーマットを VS Code / Cursor / Antigravity 等で利用可能。非商用は無料 | [公式ブログ](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 10 | Tailwind CSS | 4.2 リリース (2/19, 4.2.2 パッチ 3月) | 新カラーパレット（mauve, olive, mist, taupe）、@tailwindcss/webpack プラグイン、論理プロパティユーティリティ、font-features ユーティリティ追加 | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases) |

## Deep Dive

- [TypeScript 6.0 — JS ベース最後のリリースと 7.0 移行準備](./tu-typescript-6-0.md)
- [Vite 8.0 — Rolldown 統一バンドラーによるアーキテクチャ刷新](./tu-vite-8-rolldown.md)
