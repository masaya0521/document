# Tech Updates — 2026-04-01

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | v6.0 リリース | JavaScript ベース最後のメジャーリリース。`strict: true` デフォルト化、`module: esnext` / `target: es2025` へ変更、Temporal API 型サポート追加。Go ベースの v7.0 への橋渡し | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 2 | Vite | v8.0 リリース | Rust 製バンドラー Rolldown を統合し、esbuild + Rollup の二重構成を解消。ビルド速度 10-30x 向上、DevTools 統合、Wasm SSR サポート | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 3 | JDK | 26 GA リリース | 10 JEP を含む非 LTS リリース。HTTP/3 サポート、Structured Concurrency（6th Preview）、Ahead-of-Time Object Caching、G1 GC 改善 | [OpenJDK](https://openjdk.org/projects/jdk/26/) |
| 4 | Astro | v6.0 リリース | Vite Environment API ベースの開発サーバー刷新、Cloudflare Workers ファーストクラスサポート、CSP 組み込み API、Zod 4 移行。Node 22+ 必須 | [公式ブログ](https://astro.build/blog/astro-6/) |
| 5 | Rust | v1.94.0 リリース | `array_windows` 安定化、TOML 1.1 サポート、AVX-512 FP16 intrinsics 安定化、`LazyCell::get` / `LazyLock::get` 追加 | [Rust Blog](https://blog.rust-lang.org/2026/03/05/Rust-1.94.0/) |
| 6 | IntelliJ IDEA | 2026.1 リリース | AI エージェント（Codex, Cursor, ACP 互換）統合、Git worktree サポート、JS/TS/HTML/CSS が無料化、Dev Container ネイティブ対応 | [JetBrains Blog](https://blog.jetbrains.com/idea/2026/03/intellij-idea-2026-1/) |
| 7 | Go | v1.26 リリース | `crypto/hpke` パッケージ（RFC 9180 HPKE）追加、実験的 `simd/archsimd` パッケージ、言語構文・型システムの改善 | [Go Blog](https://go.dev/blog/go1.26) |
| 8 | Kotlin | v2.3.20 リリース | Maven プロジェクトのセットアップ簡素化、コンパイラプラグイン改善。v2.3.0 で K2 コンパイラ完全移行、名前ベースの分割代入、20-30% コンパイル高速化 | [Kotlin Blog](https://blog.jetbrains.com/kotlin/2026/03/kotlin-2-3-20-released/) |
| 9 | Tailwind CSS | v4.2.0 リリース | webpack プラグイン `@tailwindcss/webpack` 追加、4 つの新カラーパレット（mauve, olive, mist, taupe）、論理プロパティユーティリティ拡充 | [GitHub](https://github.com/tailwindlabs/tailwindcss/releases) |
| 10 | ReSharper | 2026.1 リリース | VS Code / Cursor / 互換エディタへの正式展開、ランタイムパフォーマンスモニタリングツール（CPU・メモリ監視）内蔵 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/30/resharper-2026-1-released/) |

## Deep Dive

- [TypeScript 6.0 — JavaScript ベース最後のリリース](./tu-typescript-6-0.md)
- [Vite 8.0 — Rolldown 統合による統一バンドラー](./tu-vite-8-0.md)
