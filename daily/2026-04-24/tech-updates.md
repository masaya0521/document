# Tech Updates — 2026-04-24

開発者が直接使う技術のリリース・アップデート情報を厳選して 10 件掲載します。今週は TypeScript 7.0 Beta の Go 化と Kubernetes v1.36 "Haru" が大きな話題の中心です。

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 7.0 Beta | コンパイラを Go で書き直し、10x 高速化。セマンティクスは 6.0 と同一を維持 | [Microsoft DevBlogs](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/) |
| 2 | Kubernetes | v1.36 "Haru" | 70 機能（Stable 18 / Beta 25 / Alpha 25）。User Namespaces GA、OCI VolumeSource GA、gitRepo / IPVS 削除 | [Kubernetes Blog](https://kubernetes.io/blog/2026/04/22/kubernetes-v1-36-release/) |
| 3 | Bun | v1.3.12 | ターミナルで Markdown レンダリング、Bun.WebView によるヘッドレスブラウザ、in-process `Bun.cron()` | [Bun Blog](https://bun.com/blog/bun-v1.3.12) |
| 4 | Deno | v2.7.13 | `node:repl` 実装、`node:http` を llhttp + ネイティブ TCPWrap で書き直し、Node.js 互換性強化 | [GitHub Release](https://github.com/denoland/deno/releases/tag/v2.7.13) |
| 5 | Node.js | v24.15.0 LTS 'Krypton' | LTS ラインのメンテナンスリリース。暗号関連のハンドリング改善とバグ修正 | [Node.js Releases](https://nodejs.org/en/about/previous-releases) |
| 6 | Visual Studio | 2026 April Update | JSON エディタが `$defs` / `$anchor` に対応、Copilot でテスト生成、Razor Hot Reload 高速化 | [Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 7 | Python | 3.15.0a8 / 3.14.4 | 3.15 アルファ（JIT 強化、UTF-8 デフォルト化）と 3.14 の 337 件のバグ修正メンテ | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/) |
| 8 | Go | 1.26.2 / 1.25.9 | 2026-04-07 のセキュリティ修正リリース。`archive/tar`, `crypto/tls`, `crypto/x509`, `html/template` 等 | [Go Release History](https://go.dev/doc/devel/release) |
| 9 | Chrome | 147 (Stable) | CSS `border-shape` / `contrast-color()`、WebXR Layers & Plane Detection、Web Printing API | [Chrome for Developers](https://developer.chrome.com/release-notes/147) |
| 10 | pnpm | 11 Release Candidate | SQLite バックドのストアインデックス、`minimumReleaseAge` デフォルト化、Node.js 22 以上必須 | [InfoQ](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/) |

## Deep Dive

- [TypeScript 7.0 Beta — Go 実装コンパイラで 10x 高速化](./tu-typescript-7-0-beta.md)
- [Kubernetes v1.36 "Haru" — User Namespaces GA と OCI VolumeSource](./tu-kubernetes-1-36-haru.md)

## Sources

- [Announcing TypeScript 7.0 Beta — Microsoft DevBlogs](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/)
- [Kubernetes v1.36: ハル (Haru)](https://kubernetes.io/blog/2026/04/22/kubernetes-v1-36-release/)
- [Bun v1.3.12 | Bun Blog](https://bun.com/blog/bun-v1.3.12)
- [Deno v2.7.13 Release](https://github.com/denoland/deno/releases/tag/v2.7.13)
- [Node.js Previous Releases](https://nodejs.org/en/about/previous-releases)
- [Visual Studio 2026 release notes](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes)
- [Python 3.15.0a8, 3.14.4 and 3.13.13 are out!](https://blog.python.org/2026/04/python-3150a8-3144-31313/)
- [Go Release History](https://go.dev/doc/devel/release)
- [Chrome 147 Release Notes](https://developer.chrome.com/release-notes/147)
- [pnpm 11 RC — InfoQ](https://www.infoq.com/news/2026/04/pnpm-11-rc-release/)
