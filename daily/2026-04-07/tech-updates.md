# Tech Updates — 2026-04-07

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | VS Code | 1.114 リリース | Chat UX 改善、TypeScript 6.0 対応、エンタープライズ向けポリシー制御の追加 | [Release Notes](https://code.visualstudio.com/updates/v1_114) |
| 2 | GitHub Actions | Early April 2026 アップデート | サービスコンテナの entrypoint/command オーバーライド、OIDC カスタムプロパティ GA、Azure VNET フェイルオーバー | [GitHub Changelog](https://github.blog/changelog/2026-04-02-github-actions-early-april-2026-updates/) |
| 3 | TypeScript | 6.0 リリース | JS ベース最終リリース。ES5 ターゲット廃止、Go 書き換え版（7.0）への移行準備としての破壊的変更・非推奨化を含む | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 4 | Vite | 8.0 リリース | Rolldown（Rust 製バンドラ）統合により esbuild + Rollup を置き換え。本番ビルド 10-30x 高速化（Linear: 46s → 6s） | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 5 | Astro | 6.0 リリース | Vite Environment API による dev サーバー刷新、CSP API・Fonts API・Live Content Collections の安定化、Cloudflare Workers ファーストクラス対応 | [公式ブログ](https://astro.build/blog/astro-6/) |
| 6 | JetBrains IDE | 2026.1 リリース | IntelliJ IDEA / WebStorm / PhpStorm 等一斉リリース。ACP レジストリによる AI Agent 対応、Git worktree、Wayland ネイティブ対応 | [IntelliJ Blog](https://blog.jetbrains.com/idea/2026/03/intellij-idea-2026-1/) |
| 7 | ReSharper | VS Code / Cursor 対応 | ReSharper 2026.1 で VS Code・Cursor・Google Antigravity 等の外部エディタに C# ツーリングを展開 | [JetBrains Blog](https://blog.jetbrains.com/dotnet/2026/03/30/resharper-2026-1-released/) |
| 8 | Next.js | セキュリティパッチ | CVE-2026-27979（maxPostponedStateSize 強制）、CVE-2026-29057（http-proxy パッチ）、streaming fetch ハング修正等 | [Releasebot](https://releasebot.io/updates/vercel/next-js) |
| 9 | Redis Enterprise for K8s | 8.0.16-25 メンテナンスリリース | Redis Enterprise for Kubernetes のメンテナンスリリース。前バージョン 8.0.16-24 では OSS Cluster API・ARM 対応を追加 | [Redis Docs](https://redis.io/docs/latest/operate/kubernetes/release-notes/8-0-16-releases/8-0-16-25-march2026/) |
| 10 | pnpm | 10.32 リリース | `pnpm approve-builds` に `--all` フラグ追加。10.30 では `pnpm why` がリバース依存ツリー表示にリデザイン | [GitHub Releases](https://github.com/pnpm/pnpm/releases) |

## Deep Dive

- [TypeScript 6.0 — JS ベース最終リリースと Go 書き換えへの移行](./tu-typescript-6-0.md)
- [Vite 8.0 — Rolldown 統合による 10-30x 高速化](./tu-vite-8-rolldown.md)
