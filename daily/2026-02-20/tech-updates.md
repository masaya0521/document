# Tech Updates — 2026-02-20

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Go | v1.26 リリース | Green Tea GC のデフォルト有効化、`new` 関数の拡張、ジェネリック型の自己参照サポート、cgo オーバーヘッド 30% 削減 | [公式ブログ](https://go.dev/blog/go1.26) |
| 2 | TypeScript | 6.0 Beta | JS ベース最後のリリース。strict デフォルト true 化、ES2025 / Temporal API サポート、多数のオプション非推奨化で 7.0（Go ベース）への移行準備 | [公式アナウンス](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/) |
| 3 | Astro | v6 Beta | Vite Environment API ベースの開発サーバー刷新、Cloudflare Workers ファーストクラスサポート、CSP・Live Content Collections の安定化 | [Astro Blog](https://astro.build/blog/astro-6-beta/) |
| 4 | Django | 6.0.2 セキュリティリリース | SQL インジェクション（FilteredRelation / order_by）、DoS（ASGI 重複ヘッダー / Truncator HTML パース）等 6 件のセキュリティ修正 | [Django Weblog](https://www.djangoproject.com/weblog/2026/feb/03/security-releases/) |
| 5 | PostgreSQL | 臨時リリース予告（2/26） | 2/12 リリース（18.2 等）で発生した substring() の非 ASCII テキストエラー、スタンバイ停止のリグレッション修正 | [PostgreSQL News](https://www.postgresql.org/about/news/out-of-cycle-release-scheduled-for-february-26-2026-3241/) |
| 6 | VS Code | v1.109（January 2026） | マルチエージェント開発プラットフォーム化、Claude Agent サポートプレビュー、Agent Skills GA、ターミナルサンドボックス | [リリースノート](https://code.visualstudio.com/updates/v1_109) |
| 7 | Svelte | v5.47.0 - v5.49.0 | `<select>` のCSS カスタマイズ対応、CSS パーサー（parseCss）のエクスポート、Custom Element の ShadowRootInit 設定サポート | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-february-2026) |
| 8 | Redis Enterprise for K8s | 8.0.10-21 | Redis Software 8.0.10-64 サポート、Kubernetes 環境向けの新機能・拡張を含むフィーチャーリリース | [Redis Docs](https://redis.io/docs/latest/operate/kubernetes/release-notes/8-0-10-releases/8-0-10-21-feb2026/) |
| 9 | Solidity | v0.8.34 | IR パイプラインにおけるストレージ / トランジェントストレージ変数の delete 処理の高重大度バグ修正 | [公式ブログ](https://www.soliditylang.org/blog/2026/02/18/solidity-0.8.34-release-announcement/) |
| 10 | JetBrains | Java→Kotlin 変換 VS Code 拡張 | VS Code 上でコンテキストメニューから Java ファイルを Kotlin に変換できる新しい拡張機能をリリース | [Kotlin Blog](https://blog.jetbrains.com/kotlin/2026/02/java-to-kotlin-conversion-comes-to-visual-studio-code/) |

## Deep Dive

- [Go 1.26 — Green Tea GC デフォルト化と言語仕様の改善](./tu-go-1-26.md)
- [TypeScript 6.0 Beta — JS ベース最後のリリースと 7.0 への移行準備](./tu-typescript-6-0-beta.md)
