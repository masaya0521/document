# Tech Updates — 2026-05-14

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|---|---|---|---|
| 1 | Next.js / React | セキュリティリリース (15.5.18 / 16.2.6) | 5/6・5/7 にかけて DoS・認証バイパス・SSRF・キャッシュポイズニング・XSS など 13 件の脆弱性を一括修正。全 self-host ユーザに即時アップグレード推奨 | [Vercel changelog](https://vercel.com/changelog/next-js-may-2026-security-release), [Netlify](https://www.netlify.com/changelog/2026-05-08-react-nextjs-security-vulnerabilities/) |
| 2 | Node.js | 26.0.0 / 26.1.0 (5/5・5/6 リリース) | V8 14.6 に更新。Temporal API を既定で有効化、長く非推奨だったレガシー API を削除。10 月に LTS 化予定の Current 系列 | [Node.js blog](https://nodejs.org/en/blog/release/v26.0.0) |
| 3 | Bun | v1.3.14 (5/13 リリース) | sharp 互換の組み込み画像処理 API `Bun.Image` を追加。isolated linker のグローバルストアで warm install 7 倍、HTTP/2・HTTP/3 (QUIC) を実験的サポート、Linux/macOS の `fs.watch()` を書き直し | [Bun blog](https://bun.com/blog/bun-v1.3.14) |
| 4 | PostgreSQL | 18.4 / 17.10 / 16.14 / 15.18 / 14.23 (5/11 リリース) | 全サポート系列同時のメンテナンスリリース。バグ修正中心 | [PostgreSQL Release Notes](https://www.postgresql.org/docs/release/18.0/) |
| 5 | Python | 3.14.5 (5/10 リリース) | 3.14 系の 5 回目のメンテナンス。`3.14.0`〜`3.14.4` で導入したインクリメンタル GC を、本番でのメモリ圧迫報告を受けて 3.13 と同じ世代別 GC に戻すロールバックを実施 | [Python.org](https://www.python.org/downloads/release/python-3145/) |
| 6 | Python | 3.15 beta 1 (5/11 リリース・機能凍結) | Free-threaded CPython の安定 ABI、`lazy import`、ゼロオーバーヘッドのサンプリングプロファイラ、テキストの UTF-8 既定化、JIT 高速化などを含む。GA は 10/1 予定 | [Python Insider](https://blog.python.org/2026/04/python-3150a8-3144-31313/), [PEP 790](https://peps.python.org/pep-0790/) |
| 7 | TypeScript | 7.0 Beta (4/21 ベータ、5/14 時点で VS 2026 18.6 Insiders 3 で既定化) | Go へ移植した「Project Corsa」のベータ。型チェック挙動は 6.0 と構造的に同一のまま、実プロジェクトで概ね 10 倍高速化。Visual Studio 2026 Insiders で既定有効化された | [Microsoft DevBlog](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/), [VS blog](https://devblogs.microsoft.com/visualstudio/typescript-7-beta-now-enabled-by-default-in-visual-studio-2026-18-6-insiders-3/) |
| 8 | Kubernetes | v1.36 DRA 進化のアナウンス (5/7) / v1.34.8 (5/12) | 1.36 で DRA に Prioritized List・Extended Resource・CPU/Memory への適用 (alpha) などが入り「次の時代」へ。並行して 1.34 系の 1.34.8 パッチもリリース | [DRA blog](https://kubernetes.io/blog/2026/05/07/kubernetes-v1-36-dra-136-updates/), [Patch Releases](https://kubernetes.io/releases/patch-releases/) |
| 9 | Visual Studio 2026 | 5/12 アップデート | JSON エディタが `$defs`・`$anchor` などの新しい JSON Schema 仕様に対応。Copilot エージェントが repo / user プロファイルに置かれた "agent skills" を自動発見して利用するようになった | [Visual Studio 2026 リリースノート](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 10 | HashiCorp Terraform | HCP Terraform powered by Infragraph (5/4 public preview) | HCP Terraform を Infragraph 基盤で動かす新世代を public preview として提供開始。前後して Terraform Cloud Operator for Kubernetes の GA や VSO の Kubernetes 向け強化もアナウンスされている | [HashiCorp blog](https://www.hashicorp.com/en/blog/announcing-general-availability-hashicorp-terraform-cloud-operator-for-kubernetes) |

## Deep Dive

- [Next.js + React 2026 年 5 月セキュリティリリース](./tu-nextjs-react-may-2026-security.md)
- [Node.js 26 リリース](./tu-nodejs-26.md)
