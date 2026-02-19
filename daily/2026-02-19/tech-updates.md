# Tech Updates — 2026-02-19

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Go | v1.26 リリース | Green Tea GC がデフォルト有効化、cgo オーバーヘッド約30%削減、ジェネリック型の自己参照が可能に、SIMD パッケージ（実験的）追加 | [公式ブログ](https://go.dev/blog/go1.26) |
| 2 | TypeScript | 6.0 Beta | JS ベースコンパイラの最終リリース。Temporal API 型サポート、es2025 ターゲット追加、Go ベース TS 7.0 への移行準備として `--stableTypeOrdering` フラグ導入 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/) |
| 3 | Astro | 6 Beta | Vite Environment API ベースの開発サーバー刷新、Cloudflare Workers ファーストクラスサポート、ライブコンテンツコレクション安定化、CSP サポート内蔵。Node 22+ 必須 | [InfoQ](https://www.infoq.com/news/2026/02/astro-v6-beta-cloudflare/) |
| 4 | Python | 3.14.3 / 3.13.12 | 3.14.3: 約299件のバグ修正。3.14 の主要機能にはフリースレッド Python 公式サポート (PEP 779)、t-string (PEP 750)、Zstandard 圧縮モジュール (PEP 784) を含む | [Python.org](https://www.python.org/downloads/release/python-3143/) |
| 5 | VS Code | 1.109 (January 2026) | マルチエージェント開発プラットフォーム化。複数エージェントセッションの並列実行、Claude Agent サポート、Agent Skills GA、ターミナルサンドボックス、Mermaid 図表対応 | [公式](https://code.visualstudio.com/updates/v1_109) |
| 6 | Svelte / SvelteKit | 5.47–5.49 / Kit 各種 | `<select>` 要素の CSS カスタマイズ対応 (5.47)、CSS パーサー `parseCss` 公開 (5.48)、Shadow DOM の `ShadowRootInit` 対応 (5.49)。Node/Vercel アダプタ更新 | [公式ブログ](https://svelte.dev/blog/whats-new-in-svelte-february-2026) |
| 7 | Tailwind CSS | 4.2.0 | v4.x 系の最新リリース。v4.1 で追加されたテキストシャドウ、マスクユーティリティ、旧ブラウザ互換性改善をベースに継続的改善 | [GitHub](https://github.com/tailwindlabs/tailwindcss/releases) |
| 8 | Go (セキュリティ) | 1.25.7 / 1.24.13 | go コマンドおよび crypto/tls パッケージのセキュリティ修正、crypto/x509 のバグ修正。コンパイラのバグ修正も含む | [公式](https://go.dev/doc/devel/release) |
| 9 | JetBrains IDE | 2025.3.x 各種 | GoLand 2025.3.2 (2/9)、DataGrip 2025.3.5 (2/5)、PyCharm 2025.3.2.1 (2/2) をリリース。GitHub Copilot Agent Skills がパブリックプレビューで利用可能に | [JetBrains](https://github.com/designinlife/jetbrains) |
| 10 | Redis Enterprise for K8s | 8.0.10-21 | Redis Software 8.0.10-64 をサポートするフィーチャーリリース。新機能と機能強化を含む | [公式](https://redis.io/docs/latest/operate/kubernetes/release-notes/8-0-10-releases/8-0-10-21-feb2026/) |

## Deep Dive

- [Go 1.26 — Green Tea GC・SIMD・言語仕様変更の全容](./tu-go-1-26.md)
- [TypeScript 6.0 Beta — JS ベース最終リリースと TS 7.0 への移行準備](./tu-typescript-6-0-beta.md)
