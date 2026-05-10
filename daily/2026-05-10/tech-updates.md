# Tech Updates — 2026-05-10

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Next.js / React | 16.2.6 / 15.5.18 + RSC patch | 12 件の脆弱性を一斉修正。CVE-2026-23870 を含む RSC の DoS、ミドルウェア / プロキシバイパス、SSRF、キャッシュポイズニング、XSS など。App Router 利用者は即時アップグレード推奨 | [Vercel changelog](https://vercel.com/changelog/next-js-may-2026-security-release), [ZeroPath blog](https://zeropath.com/blog/cve-2026-23870-react-server-components-dos) |
| 2 | Go | 1.26.3 / 1.25.10 | 11 件のセキュリティ修正を含むパッチリリース。`go` コマンドの module proxy checksum バイパス、`pack` のパストラバーサル、`net/mail` の DoS、Windows での NUL バイトパニックを修正 | [golang-announce](https://groups.google.com/g/golang-announce/c/qcCIEXso47M) |
| 3 | Python | 3.14.5 | 約 113 件のバグ修正。最大の変更点は incremental GC を本番でのメモリ圧迫の問題で 3.13 系の generational GC へ revert。uuid v3/v5 が最大 40% 高速化、UUID v6-v8 を完全サポート | [Python Insider](https://blog.python.org/2026/05/python-3145rc1/), [python.org](https://www.python.org/downloads/release/python-3145rc1/) |
| 4 | VS Code | 1.117 | Copilot Business / Enterprise の BYOK（OpenRouter / Ollama / OpenAI 等）、Copilot CLI ランチャー、Claude Code / Gemini CLI 含む agent CLI のターミナルタイトル検出、TypeScript 6.0.3 同梱 | [VS Code 1.117](https://code.visualstudio.com/updates/v1_117) |
| 5 | pnpm | 11.0 | サプライチェーン保護のデフォルト強化（`minimumReleaseAge=1440`、`blockExoticSubdeps=true`）、JSON-per-package store を SQLite に置換、ESM-only 化、Node.js 22 以上必須 | [pnpm blog](https://pnpm.io/blog/releases/11.0), [InfoQ](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/) |
| 6 | Cloudflare Workers | Stream Bindings & Tracing | Workers から Stream 動画のアップロード・signed playback URL 生成を非認証 API なしで実行可能に。OpenTelemetry 連携の Workers Tracing が Wrangler 設定で有効化可能 | [Cloudflare changelog](https://developers.cloudflare.com/changelog/) |
| 7 | Docker | Engine v29.3.0 / Desktop | Docker Model Runner OCI Registry Client の SSRF 脆弱性 CVE-2026-33990 を修正。NVIDIA Container Toolkit v1.19.0 同梱、MCP プロファイルテンプレートカードと Logs (Beta) ビューを追加 | [Docker release notes](https://releasebot.io/updates/docker) |
| 8 | Bun | 1.3.11 | 105 件の Issue を修正、Linux バイナリが 4MB スリム化。`Bun.cron` で OS レベル cron / 式パーサー、`Bun.sliceAnsi` で ANSI / grapheme aware な slicing、`bun test --path-ignore-patterns`、Windows ARM64 native `.bin` shim 追加 | [Bun blog](https://bun.com/blog) |
| 9 | CodeQL | 2.25.3 | Swift 6.3 サポートを追加。default code scanning suite に C/C++ クエリ 5 種を昇格。各言語で精度改善 | [GitHub changelog](https://releasebot.io/updates/github) |
| 10 | Kubernetes | v1.36 "Haru" | 70 件の機能改善（18 Stable / 25 Beta / 25 Alpha）。5/20 にリリースハイライト webinar が予定 | [Kubernetes blog](https://kubernetes.io/blog/2026/04/22/kubernetes-v1-36-release/) |

## Deep Dive

- [Next.js / React 2026年5月セキュリティ一括修正](./tu-nextjs-react-may-2026-security.md)
- [pnpm 11 — サプライチェーン防御を既定化、SQLite ストアと ESM 化](./tu-pnpm-11.md)
