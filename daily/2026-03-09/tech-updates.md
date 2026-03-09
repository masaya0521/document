# Tech Updates — 2026-03-09

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Rust | v1.94.0 リリース | array_windows API、数学定数（EULER_GAMMA, GOLDEN_RATIO）の追加、AVX-512 FP16 安定化、Cargo の include キーと TOML 1.1 サポート | [Rust Blog](https://blog.rust-lang.org/2026/03/05/Rust-1.94.0/) |
| 2 | Deno | v2.7.0 リリース | Temporal API の安定化、Windows ARM サポート、npm package.json overrides 対応、V8 14.5 へアップグレード | [Deno Blog](https://deno.com/blog/v2.7) |
| 3 | Go | v1.26.1 リリース | crypto/x509, html/template, net/url, os パッケージのセキュリティ修正とバグフィックス | [Go Blog](https://go.dev/blog/go1.26) |
| 4 | VS Code | v1.110 リリース | Agent Plugins、Agentic Browser Tools、Kitty グラフィクスプロトコル対応、セッションメモリ改善 | [VS Code Updates](https://code.visualstudio.com/updates/v1_108) |
| 5 | TypeScript | v6.0 Beta | Go ベースコンパイラ（Corsa）移行前の最後の JS ベースリリース。5-10x 高速化への布石 | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/) |
| 6 | Svelte | v5.53.0 + SvelteKit v2.51.0 | Error boundaries のサーバーサイド対応、ナビゲーションコールバックにスクロール位置情報を追加 | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-march-2026) |
| 7 | Go | v1.26.0（2月リリース） | Green Tea GC デフォルト化、30% 高速化した cgo 呼び出し、new(expression) 構文、実験的 SIMD intrinsics、crypto/hpke | [Go Blog](https://go.dev/blog/go1.26) |
| 8 | Python | v3.14.3 メンテナンスリリース | 299件のバグ修正。Python 3.14 系の安定性向上（t-strings, Free-threaded Python, deferred annotations 等が利用可能） | [Python.org](https://www.python.org/downloads/release/python-3143/) |
| 9 | React | v19.2（2025年10月リリース、Next.js 16 経由で普及中） | Activity コンポーネント、useEffectEvent フック、Partial Pre-rendering、Performance Tracks | [React Blog](https://react.dev/blog/2025/10/01/react-19-2) |
| 10 | Visual Studio 2026 | v18.3 リリース | AI ネイティブ IDE として Profiler Agent、Debugger Agent を搭載。.NET 10 完全対応 | [Visual Studio Magazine](https://www.i-programmer.info/news/90-tools/18674-visual-studio-2026-183-released.html) |

## Deep Dive

- [Rust 1.94.0 — array_windows と Cargo include](./tu-rust-1-94.md)
- [Deno 2.7 — Temporal API 安定化と Windows ARM サポート](./tu-deno-2-7.md)
