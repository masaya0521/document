# Tech Updates — 2026-05-11

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Next.js | 16.2.6 / 15.5.18 セキュリティリリース | 13 件のアドバイザリを一括修正。RSC の DoS（CVE-2026-23870）、Cache Components の接続枯渇 DoS、WebSocket アップグレードでの SSRF、RSC レスポンスのキャッシュポイズニング、App Router の CSP nonce 周りの XSS。アップデート以外の緩和策なし | [Vercel changelog](https://vercel.com/changelog/next-js-may-2026-security-release), [Netlify まとめ](https://www.netlify.com/changelog/2026-05-08-react-nextjs-security-vulnerabilities/) |
| 2 | Go | 1.25.10 / 1.26.3（2026-05-07） | 11 件のセキュリティ修正。`go` コマンドの checksum DB バイパス（CVE-2026-42501）、`go tool pack` のパストラバーサル（CVE-2026-39817）、`net.Dial`/`LookupPort` の Windows panic（CVE-2026-39836）、`net/mail` の `consumePhrase` DoS（CVE-2026-42499）など | [golang-announce](https://groups.google.com/g/golang-announce/c/qcCIEXso47M) |
| 3 | Python | 3.14.5（2026-05-08） | 5回目のメンテナンスリリース。**3.14.0〜3.14.4 に入っていたインクリメンタル GC を撤回し 3.13 の世代別 GC へロールバック**。本番でメモリ圧迫の報告が相次いだことが理由。約 113 件のバグ/ビルド/ドキュメント修正 | [Python Insider](https://blog.python.org/2026/05/python-3145rc1/), [python.org](https://www.python.org/downloads/release/python-3145rc1/) |
| 4 | VS Code | 1.118（2026 年 5 月） | Copilot CLI セッションの GitHub.com / モバイルからのリモートコントロール、ワークスペース横断のセマンティックコードベース検索、スキル実行を分離する dedicated context、Anthropic モデル向けキャッシュ再利用でリピートコンテキストのトークンレートが **約 10 分の 1** に | [VS Code 1.118](https://code.visualstudio.com/updates/v1_118), [Neowin](https://www.neowin.net/news/microsoft-updates-vs-code-to-1118-and-adds-remote-control-for-copilot-cli/) |
| 5 | Astro | 6.3 / 6.3.1（2026-05-07） | experimental advanced routing を追加。Hono など fetch ハンドラ系フレームワークを first-class で組み込み可能。i18n.fallback の空レスポンスや `session.delete()` 初回呼び出し時の永続化バグも修正 | [Astro 6.3 ブログ](https://astro.build/blog/astro-630/) |
| 6 | Svelte / SvelteKit | 2026 年 5 月のアップデート | SvelteKit が TypeScript 6.0 を正式サポート、Remote functions が hydratable な transport を使用、`form.enhance` の submit が成否を boolean で返却、form フィールドが `field.as(type, value)` でデフォルト値を指定可能。`svelte/motion` から `TweenOptions` / `SpringOptions` 型をエクスポート（5.55.0） | [What's new in Svelte: May 2026](https://svelte.dev/blog/whats-new-in-svelte-may-2026) |
| 7 | Docker Desktop | 2026 年 5 月リリース | AI アシスタント "Gordon" が永続ローカルメモリを獲得。MCP プロファイルテンプレートカードとオンボーディングツアー、Model Runner で Qwen3.5 をサポート、Logs(Beta) で Compose スタック単位のフィルタ。**CVE-2026-33990**（Docker Model Runner OCI Registry Client の SSRF）も修正 | [Docker Desktop release notes](https://docs.docker.com/desktop/release-notes/) |
| 8 | HCP Terraform | Infragraph 版 public preview（2026-05-04） | HashiCorp が「Infragraph 駆動」の HCP Terraform を public preview として公開。インフラ依存関係グラフを核に、複数プロバイダ・モジュール横断の解析や影響範囲の可視化を強化 | [HashiCorp blog（Releasebot まとめ）](https://releasebot.io/updates/docker) |
| 9 | Redis | Redis Software 8.0.18-36（2026 年 5 月） / Redis OS 8.6 RC1 | Redis Software 8.0.18-36 がリリースされ、Redis Open Source 8.6 / 8.4 / 8.2 / 8.0 / 7.4 / 7.2 / 6.2 をサポート。Redis Open Source 8.6 は feature-complete な RC で、ベクトル検索や JSON 関連の改善を含む | [Redis Software 8.0.18-36](https://redis.io/docs/latest/operate/rs/release-notes/rs-8-0-releases/rs-8-0-18-36/), [Redis 8.6 What's new](https://redis.io/docs/latest/develop/whats-new/8-6/) |
| 10 | Bun | v1.3.13（2026-04-19） | 82 件の修正。`bun install` がレジストリ tarball をディスクへストリーム化し大規模リポジトリで **メモリ使用量 17 倍削減**、ソースマップのメモリ 8 倍削減 + zlib-ng で gzip 5.5 倍高速化、`bun test` に `--isolate` / `--parallel[=N]` を追加、`Bun.serve()` で Range リクエスト対応、JavaScriptCore に 1,316 件の upstream コミットをマージ | [Bun v1.3.13](https://bun.com/blog/bun-v1.3.13), [GitHub Release](https://github.com/oven-sh/bun/releases/tag/bun-v1.3.13) |

## Deep Dive

- [Next.js 2026 年 5 月コーディネートセキュリティリリース（13 アドバイザリ）](./tu-nextjs-may-2026-security.md)
- [Go 1.25.10 / 1.26.3 セキュリティリリース（CVE 11 件）](./tu-go-1-25-10-security.md)
