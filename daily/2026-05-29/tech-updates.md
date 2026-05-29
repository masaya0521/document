# Tech Updates — 2026-05-29

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | VS Code | v1.122 リリース（5/28） | GitHub サインイン不要の「Air-gapped BYOK」、統合ブラウザのデバイスエミュレーション、スクリーンショット添付、リッチな Issue 報告ウィザードを追加 | [Release Notes](https://code.visualstudio.com/updates/v1_122) |
| 2 | PostgreSQL | 18.4 / 17.10 / 16.14 / 15.18 / 14.23（5/14） | 全サポートブランチへの定例アップデート。累積バグ修正とセキュリティ修正を含む四半期リリース | [Release Notes](https://www.postgresql.org/docs/release/) |
| 3 | SvelteKit | 2.57.0 / 2.56.0（5月） | TypeScript 6.0 対応、`field.as(type, value)` でフォームの初期値指定、remote functions の transport が hydratable 化、`sv` CLI でコミュニティ add-on を実験提供 | [What's new in Svelte](https://svelte.dev/blog/whats-new-in-svelte-may-2026) |
| 4 | Nuxt | 4.4.6 / 3.21.6（5/18） | パッチリリース。SSR モジュールキャッシュの無効化修正など複数のバグ修正。4.4 系では custom useFetch/useAsyncData factory や vue-router v5 対応も | [Changelog](https://nuxt.com/changelog) |
| 5 | FastAPI | 0.136.3（5/23） | パッチリリース。依存解決・ドキュメント・型まわりの改善を含む継続的アップデート | [GitHub Releases](https://github.com/fastapi/fastapi/releases) |
| 6 | Docker Desktop | 5月アップデート | MCP プロファイルテンプレートカードとオンボーディングツアー追加、Compose スタック単位のログフィルタ改善、Model Runner の Qwen3.5 対応。CVE-2026-33990 のセキュリティ修正 | [Release Notes](https://docs.docker.com/desktop/release-notes/) |
| 7 | Next.js | バックポートのバグ修正・セキュリティ更新 | streaming fetch ハング修正、`maxPostponedStateSize` 強制（CVE-2026-27979）、http-proxy パッチ（CVE-2026-29057）、image LRU ディスクキャッシュ追加 | [Next.js Updates](https://nextjs.org/blog) |
| 8 | Rust | 1.96.0 ベータ / 1.95.0 安定版 | 6 週間サイクルを継続。1.96.0 が 5/28 時点でベータ。`str::contains` の aarch64 高速化やセキュリティパッチを含む | [Release Announcements](https://blog.rust-lang.org/releases/) |
| 9 | KernelScript | OSS Summit で発表（ベータ） | eBPF・ユーザー空間・カーネル拡張開発を型安全な 1 言語に統合する Linux カーネル向け DSL。Multikernel Technologies の Cong Wang 氏が発表 | [Phoronix](https://www.phoronix.com/news/KernelScript) |
| 10 | Wasp | Launch Week（TypeScript SDK） | 「JS 版 Rails/Laravel」を標榜するフルスタックフレームワーク。独自言語をやめ TypeScript SDK を主要な利用方法として提供する方針を表明 | [Wasp Blog](https://wasp.sh/blog/2026/05/13/new-language-for-web-dev-was-a-mistake) |

## Deep Dive

- [VS Code 1.122 — エージェント・BYOK・統合ブラウザの強化](./tu-vscode-1-122.md)
- [SvelteKit 2026年5月アップデート — remote functions と TypeScript 6.0 対応](./tu-sveltekit-may-2026.md)
