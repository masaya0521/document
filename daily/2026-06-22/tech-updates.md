# Tech Updates — 2026-06-22

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 7.0 RC リリース（6/18） | Go ネイティブ実装の新コンパイラ（Project Corsa）が RC 到達。型チェックが従来比 約10倍高速、VS Code のコードベースで 77秒→7.5秒。安定版 GA は約1ヶ月以内を予定 | [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/04/21/typescript-7-0-beta-arrives-on-go-based-foundation-with-10x-speed-claim.aspx), [公式 Beta 告知](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/) |
| 2 | Node.js | セキュリティリリース（6/18） | 26.x / 24.x / 22.x の各系列でセキュリティ修正。最高深刻度 HIGH。WebCrypto のクラッシュ、TLS ワイルドカード認証バイパス、Permission Model バイパス、HTTP/2 ORIGIN フレームによる OOM を修正 | [Node.js Blog](https://nodejs.org/en/blog/vulnerability/june-2026-security-releases) |
| 3 | VS Code | 1.125 リリース（6/17） | 統合ブラウザの強化（リモート接続越しの安全なブラウジング）、Marketplace 経由のモデルプロバイダ追加、拡張機能更新の遅延制御、MDM 経由の Copilot ポリシー配信 | [Release Notes](https://code.visualstudio.com/updates/v1_125) |
| 4 | PostgreSQL | 19 Beta 1 リリース（6/4） | PG18 から200以上の変更。SQL/PGQ プロパティグラフクエリ、`ON CONFLICT DO SELECT`、`REPACK` コマンド、並列 autovacuum、外部キーチェック2倍高速化、データチェックサムのオンライン切替、JIT デフォルト無効化 | [公式ニュース](https://www.postgresql.org/about/news/postgresql-19-beta-1-released-3313/) |
| 5 | Python | 3.15 フィーチャーフリーズ / 3.15.0b2（6月） | 3.15 が6月にフィーチャーフリーズ・Beta 段階入り（3.15.0b2 が 6/2 リリース）。今後は安定化・バグ修正フェーズへ。秋の正式リリースに向け調整 | [Real Python](https://realpython.com/python-news-june-2026/), [PEP 790](https://peps.python.org/pep-0790/) |
| 6 | Django | 6.0 メジャーリリース | モダンな Python サポート（3.10+ 必須）、セキュリティデフォルト強化、DB 機能改善、多数の QoL 向上を含むメジャーアップデート | [VersionLog](https://versionlog.com/django/6.0/) |
| 7 | Vite | 8.0 リリース | Vite Devtools を有効化する devtools オプションを追加。Vue / Nuxt / Svelte / Solid / Astro 等の標準バンドラとしてエコシステム全体に影響 | [Vite Blog](https://vite.dev/blog/announcing-vite8) |
| 8 | Astro | 6.4 リリース | Rust 製の新 Markdown プロセッサ「Sätteri」を導入。大規模ドキュメントサイトのビルド時間を1分以上短縮 | [Astro](https://astro.build/) |
| 9 | Bun | 1.3 リリース | ゼロコンフィグのフロントエンド開発（`bun index.html` で自動配信・ESM 解決・HMR）。Vite/Webpack 不要。Claude Code のランタイムとしても採用 | [LogRocket](https://blog.logrocket.com/bun-javascript-runtime-taking-node-js-deno/) |
| 10 | Angular | 22 リリース（5/16） | 「Signal-First」時代へ。Signal Forms / Signals API が安定化、Selectorless Components、Zoneless アーキテクチャ深化、新規コンポーネントは OnPush がデフォルト | [angular.dev](https://angular.dev/events/v22) |

## Deep Dive

- [TypeScript 7.0 RC — Go ネイティブコンパイラ（Project Corsa）](./tu-typescript-7-0-rc.md)
- [PostgreSQL 19 Beta 1 — 主要新機能まとめ](./tu-postgresql-19-beta1.md)
