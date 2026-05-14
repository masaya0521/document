# Tech Updates — 2026-05-15

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Python | 3.15.0 beta 1 リリース（feature freeze） | PEP 810 の lazy imports、free-threaded ビルド向けの安定 ABI（abi3t）、新しい Tachyon サンプリングプロファイラ、JIT の x86-64 Linux で約 8-9% / Apple Silicon で 12-13% の性能改善 | [Python Insider](https://blog.python.org/2026/05/python-3150-beta-1/), [The Register](https://www.theregister.com/devops/2026/05/11/feature-freeze-for-python-315-as-first-beta-released/) |
| 2 | Python | 3.14.5 メンテナンスリリース | 154 件のバグ修正、ビルド改善、ドキュメント更新。3.14.0〜3.14.4 で導入されていたインクリメンタル GC を本番でのメモリ圧迫の報告を受け 3.13 の世代別 GC に差し戻し | [Python.org](https://www.python.org/downloads/release/python-3145/), [Python Insider](https://blog.python.org/2026/05/python-3145rc1/) |
| 3 | PostgreSQL | 18.4 / 17.10 / 16.14 / 15.18 / 14.23 マイナーリリース | standby が "could not access status of transaction" で停止する問題、非 ASCII で substring() がエラーになる問題、json_strip_nulls() / jsonb_strip_nulls() の関数 volatility 修正等 | [PostgreSQL](https://www.postgresql.org/) |
| 4 | Go | 1.25.10 / 1.26.3 セキュリティリリース | `go` コマンド、`pack` ツール、`html/template`, `net`, `net/http`, `net/http/httputil`, `net/mail`, `syscall` パッケージのセキュリティ修正と、コンパイラ・リンカ・ランタイム等のバグ修正 | [Go Release History](https://go.dev/doc/devel/release) |
| 5 | Angular | 22.0-rc.0 リリース | Selectorless Components（テンプレートでクラスを直接 import）、Signal-based Forms の正式安定化、Zoneless がデフォルト、Angular CLI が Vitest をデフォルトテストランナーに、TypeScript 5.9 対応 | [Medium (Angular Engineering)](https://medium.com/angular-engineering/angular-22-the-shift-to-signal-first-zoneless-and-performance-driven-architecture-b0d5a68f51e6), [VersionLog](https://versionlog.com/angular/22.0/) |
| 6 | Next.js | 協調的セキュリティリリース | DoS、ミドルウェア/プロキシバイパス、SSRF、キャッシュポイズニング、XSS など 13 件のアドバイザリに対応。streaming fetch ハング修正、`maxPostponedStateSize` 強制（CVE-2026-27979）、http-proxy パッチ（CVE-2026-29057）等 | [Vercel Changelog](https://vercel.com/changelog/next-js-may-2026-security-release) |
| 7 | Svelte / SvelteKit | 2026 年 5 月アップデート | TypeScript 6.0 対応、フォームフィールドの `field.as(type, value)` で初期値指定可、remote function transport が hydratable を採用してクエリ結果でリッチなデータ型をサポート、`sv` CLI でコミュニティアドオンが experimental 提供 | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-may-2026) |
| 8 | VS Code | 1.120 リリース | Agents Window が Stable に昇格、BYOK モデルのトークン利用量トラッキングと thinking effort 設定、Markdown 差分のプレビュー、ターミナルコマンドのリスク評価、ターミナル出力の圧縮 | [VS Code Release Notes](https://code.visualstudio.com/updates/v1_120) |
| 9 | GitHub Actions | windows-latest / windows-2025 を Visual Studio 2026 に移行、Arm64 ランナーを内製化 | `windows-latest` / `windows-2025` ラベルが既定で VS 2026 を使うように変更（6/8 開始・6/15 完了予定）。Arm64 ランナーイメージのメンテナンスを GitHub が引き継ぎ | [GitHub Changelog](https://github.blog/changelog/2026-05-14-github-actions-upcoming-image-migrations/) |
| 10 | GitHub CodeQL | 2.25.4 リリース | Swift 6.3.1 のサポート追加、C# と Java の解析改善等 | [GitHub Changelog](https://github.blog/changelog/2026-05-12-codeql-2-25-4-adds-swift-6-3-1-support-improvements-to-c-and-java-and-more/) |

## Deep Dive

- [Python 3.15.0 beta 1 — feature freeze と lazy imports / 安定 free-threaded ABI / Tachyon プロファイラ](./tu-python-3-15-beta1.md)
- [Angular 22.0-rc.0 — Selectorless Components と Signal-first 時代の到来](./tu-angular-22-rc.md)
