# Tech Updates — 2026-04-23

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Kubernetes | v1.36 リリース（4/22） | 約80件の Enhancement。User Namespaces / MutatingAdmissionPolicy / OCI VolumeSource / HPA Scale-to-Zero などが GA。`gitRepo` ボリュームと kube-proxy の IPVS モードを削除 | [Kubernetes Blog (Sneak Peek)](https://kubernetes.io/blog/2026/03/30/kubernetes-v1-36-sneak-peek/) |
| 2 | Rust | 1.95.0 リリース（4/16） | `cfg_select!` マクロ追加、match の if-let ガード安定化、API 拡張。stable で `rustc` への custom target 指定を不可化 | [Rust Blog](https://blog.rust-lang.org/2026/04/16/Rust-1.95.0/) |
| 3 | Visual Studio Code | 1.113 リリース（4月） | チャット周りを大幅刷新（unified chat customizations、reasoning effort 設定、ネスト sub-agent、CLI MCP/デバッグログ）。新しい Light/Dark テーマ | [Releasebot — VS Code](https://releasebot.io/updates/microsoft/visual-studio-code) |
| 4 | Python | 3.14.4 / 3.15.0a8（4/7） | 3.14 系のメンテナンスリリースと、3.15 の最終アルファ。3.15 は次回 5/5 のベータで機能追加が締め切られる | [Python Insider Blog](https://blog.python.org/2026/04/python-3150a8-3144-31313/) |
| 5 | pnpm | 11 Release Candidate（4月） | SQLite ベースの新ストアフォーマット、`minimumReleaseAge=1d` などのサプライチェーン強化、ビルドスクリプト設定を `allowBuilds` に統一 | [InfoQ](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/) |
| 6 | Bun | v1.3.13 リリース（4月中旬） | `bun install` がストリーミングで tarball を展開しメモリを17倍削減、`bun test` の `--parallel/--isolate/--shard/--changed`、zlib-ng で gzip 5.5倍高速化 | [Bun Blog](https://bun.com/blog/bun-v1.3.13) |
| 7 | Deno | 2.7.12 リリース（4/22） | 直近の 2.7 系メンテナンスリリース。LTS 2.5 のサポートは 4/30 で終了予定 | [GitHub Releases](https://github.com/denoland/deno/releases) |
| 8 | JetBrains PyCharm | 2026.1 リリース | デバッガーエンジンを debugpy へ刷新、リモートターゲットでの uv ファーストクラスサポート | [JetBrains Blog (Releases)](https://blog.jetbrains.com/category/releases/) |
| 9 | Tailwind CSS | v4.1 リリース | `text-shadow-*` / `mask-*` ユーティリティ、カラー drop-shadow、論理プロパティ `pbs-*`/`mbs-*`/`inline-*`、古い Safari/Firefox 向けフォールバック | [Tailwind Blog](https://tailwindcss.com/blog/tailwindcss-v4-1) |
| 10 | WordPress | `@wordpress/build` 公開（4月） | 既存の Webpack + Babel パイプラインを esbuild ベースに置き換え。`package.json` から PHP 登録ファイルを自動生成 | [WP Developer News](https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/) |

## Deep Dive

- [Kubernetes v1.36 — Stability・Compatibility・Reproducibility 重視のリリース](./tu-kubernetes-1-36.md)
- [Rust 1.95 — `cfg_select!` と if-let ガードで pattern matching を強化](./tu-rust-1-95.md)
