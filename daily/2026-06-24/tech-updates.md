# Tech Updates — 2026-06-24

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 7.0 RC リリース（6/18） | Go ネイティブコンパイラ（Project Corsa / tsgo）が RC 到達。型チェックが約 10 倍高速化、メモリ約半減。GA は約 1 ヶ月後の見込み | [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/03/23/typescript-6-0-ships-as-final-javascript-based-release-clears-path-for-go-native-7-0.aspx), [microsoft/typescript-go](https://github.com/microsoft/typescript-go) |
| 2 | VS Code | 1.125.1 リリース（6/18） | 統合ブラウザ（リモート接続でも Web 検索・閲覧可能）、拡張機能の自動更新遅延を設定可能に、Copilot のエンタープライズ管理強化 | [Releasebot](https://releasebot.io/updates/microsoft/visual-studio-code) |
| 3 | Next.js | 16.2.7 が最新安定版（6/10 時点） | 16.2 系はバグ修正・安定化中心のバックポートリリース。hydration / router 修正、cache tag エンコード改善、Server Action・middleware 修正、Turbopack 変更、FormData ハンドリング改善 | [Releasebot](https://releasebot.io/updates/vercel/next-js) |
| 4 | Nuxt UI | 4.9.0 リリース（6/4） | フォームで `name` 属性設定をサポート、InputMenu / SelectMenu のハイライト不具合を修正 | [Nuxt UI Releases](https://ui.nuxt.com/releases) |
| 5 | Astro | 6.4.4 が最新安定版（6 月時点） | v6.0 系は開発サーバ・本番バンドラを Vite 7.0 に更新。コンテンツ駆動サイト向けにゼロ JS デフォルトを継続 | [Astro Docs](https://docs.astro.build/en/guides/upgrade-to/v6/) |
| 6 | Deno | 2.8 リリース（5/22） | 「過去最大のマイナーリリース」。依存脆弱性の自動修正、deno.json/package.json のバージョン更新コマンド、npm 公開用 tarball 生成、V8 を 14.9 へ、Node テスト互換 42%→76.4% | [Deno Blog](https://deno.com/blog/v2.8) |
| 7 | PostgreSQL | 18.4 / 17.10 / 16.14 / 15.18 / 14.23（5/14） | 全サポートバージョンへの定期更新。11 件のセキュリティ脆弱性と 60 件超のバグを修正 | [PostgreSQL News](https://www.postgresql.org/about/news/postgresql-184-1710-1614-1518-and-1423-released-3297/) |
| 8 | Ruby | 4.0.5 リリース（5/20） | 4.0 系の安定版パッチリリース | [Ruby Releases](https://www.ruby-lang.org/en/downloads/releases/) |
| 9 | Kubernetes | 1.36.1 が最新（5/13） | 1.36 系の最初のパッチリリース。EOL は 2027-06-28 | [Kubernetes Releases](https://kubernetes.io/releases/) |
| 10 | Redis（node-redis / Redis Insight） | RESP3 デフォルト化 / Insight 3.4.1 GA | node-redis が RESP3 デフォルトへ移行し Redis 8.8 コマンド対応・cluster/pubsub 信頼性修正。Redis Insight 3.4.1 GA は専用 Search ワークスペース、Linux ARM64 対応 | [redis/redis Releases](https://github.com/redis/redis/releases) |

## Deep Dive

- [TypeScript 7.0 RC — Go ネイティブコンパイラ（Project Corsa）](./tu-typescript-7-0-rc.md)
- [Deno 2.8 — 過去最大のマイナーリリース](./tu-deno-2-8.md)
