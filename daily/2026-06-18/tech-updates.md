# Tech Updates — 2026-06-18

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Visual Studio Code | v1.125 リリース（6/17） | 統合ブラウザのWeb検索・リモートプロキシ対応、拡張機能の自動更新遅延設定、MDM 経由の Copilot 管理設定、LSP 3.18 対応 | [Release Notes](https://code.visualstudio.com/updates/v1_125) |
| 2 | Angular | v22 リリース（6/3） | OnPush がデフォルト変更検知に、Signal Forms が安定化、Resource API（resource/httpResource）安定化、`@Service` デコレータ追加 | [dev.to](https://dev.to/rigole/angular-22-is-here-everything-you-need-to-know-4g3c), [endoflife](https://endoflife.date/angular) |
| 3 | Next.js | v16.2 系 | Cache Components（`use cache` を file/function/component 単位で適用）、dev サーバ起動が 16.1 比 約87%高速化、ImageResponse 2〜20x 高速化、Build Adapters 安定化 | [公式ブログ](https://nextjs.org/blog/next-16-2), [GitHub](https://github.com/vercel/next.js/releases) |
| 4 | Tailwind CSS | v4.3.1 リリース（6/12） | `--silent` CLI オプション追加、Node 26+ 非推奨警告の修正、`@apply` の CSS mixin 対応、container query 向け `not-*` 修正 | [GitHub](https://github.com/tailwindlabs/tailwindcss/releases) |
| 5 | Python | 3.14.6 リリース（6/10） | 3.14 系のバグfixリリース。並行して 3.15 がフィーチャーフリーズ入り（最終リリースは10月予定） | [Python Insider](https://blog.python.org/), [Real Python](https://realpython.com/python-news-june-2026/) |
| 6 | Astro | v6.4 系 | Rust 製 Markdown プロセッサ「Sätteri」を導入し、大規模ドキュメントサイトのビルドを大幅短縮 | [GitHub](https://github.com/withastro/astro/releases) |
| 7 | node-redis | v6 リリース | 5.x 以来のメジャー。RESP3 をデフォルトプロトコル化、Redis 8.8 コマンド網羅、pubsub/cluster の信頼性改善、最低 Node.js バージョン引き上げ | [GitHub](https://github.com/redis/node-redis/releases) |
| 8 | Laravel | 12.x / 13.x アップデート | Vite フォントマニフェストから自動で web フォントを読み込む `@fonts` Blade ディレクティブ、S3 等の既存ディスクを KV キャッシュに使えるファイルシステムキャッシュドライバ追加 | [Releasebot](https://releasebot.io/updates/laravel) |
| 9 | Django | 6.1 開発版 | N+1 問題に対処する `FETCH_PEERS`（兄弟インスタンスの未取得フィールドを一括取得し 101 クエリ→2 クエリに削減）を導入 | [VersionLog](https://versionlog.com/django/6.1/) |
| 10 | Redis Insight | v3.4.1 GA | 専用の Search ワークスペース（インデックスのライフサイクル全対応）追加、Azure 連携強化（Entra ID Docker 対応、Access Key 認証） | [Redis Docs](https://redis.io/docs/latest/develop/tools/insight/) |

## Deep Dive

- [Angular 22 — signal-first 時代へ](./tu-angular-22.md)
- [Next.js 16.2 — Cache Components と use cache](./tu-nextjs-16-2.md)
