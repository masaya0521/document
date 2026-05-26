# Next.js / React May 2026 セキュリティリリース — 13 CVE の全容

- **日付**: 2026-05-06（フォローアップ 05-07）
- **カテゴリ**: Frontend / Backend
- **ソース**: [Vercel Changelog](https://vercel.com/changelog/next-js-may-2026-security-release), [Netlify Changelog](https://www.netlify.com/changelog/2026-05-08-react-nextjs-security-vulnerabilities/), [Cloudflare Changelog](https://developers.cloudflare.com/changelog/post/2026-05-06-react-nextjs-vulnerabilities/)

## 概要

Next.js と React チームによる協調セキュリティリリース。Next.js で 11件、React Server Components で 1件（CVE-2026-23870）、フォローアップで 1件の計 13件のセキュリティアドバイザリが公開・修正された。DoS、ミドルウェア/プロキシバイパス、SSRF、キャッシュポイズニング、XSS と攻撃ベクトルは多岐にわたる。

## 脆弱性カテゴリ別の概要

### Middleware / Proxy バイパス（5件）

| 深刻度 | 概要 |
|--------|------|
| High (4件) | `middleware.js` / `proxy.js` によるアクセス制御をバイパスする脆弱性。認可ロジックをミドルウェアに依存するアプリケーションが影響を受ける |
| Low (1件) | ミドルウェアリダイレクト時のキャッシュポイズニングリスク |

### Denial of Service（3件）

| 深刻度 | CVE | 概要 |
|--------|-----|------|
| High | CVE-2026-23870 | React Server Components のデシリアライズ時に過剰な CPU 使用を引き起こす DoS |
| High | CVE-2026-23869 | App Router Server Function エンドポイントへの細工されたリクエストによる DoS |
| Moderate | — | Image Optimization API に対する DoS |

### Server-Side Request Forgery（1件）

| 深刻度 | CVE | 概要 |
|--------|-----|------|
| High | CVE-2026-44578 | WebSocket アップグレードリクエスト処理における SSRF。認証なしで内部リソースにアクセス可能 |

### Cache Poisoning（2件）

| 深刻度 | 概要 |
|--------|------|
| — | React Server Component のレスポンスキャッシュレイヤーを標的にしたキャッシュポイズニング |

### Cross-Site Scripting（2件）

| 深刻度 | 概要 |
|--------|------|
| Moderate | CSP nonce 処理の脆弱性 |
| Moderate | `beforeInteractive` スクリプトにおける XSS |

## 影響バージョンと修正バージョン

| パッケージ | 影響バージョン | 修正バージョン |
|-----------|---------------|---------------|
| Next.js 13〜14.x | 全バージョン | 15.5.18 または 16.2.6 へアップグレード |
| Next.js 15.x | ≤ 15.5.17 | **15.5.18** |
| Next.js 16.x | ≤ 16.2.5 | **16.2.6** |
| react-server-dom-parcel | 19.x 系 | 19.0.6 / 19.1.7 / 19.2.6 |
| react-server-dom-webpack | 19.x 系 | 19.0.6 / 19.1.7 / 19.2.6 |
| react-server-dom-turbopack | 19.x 系 | 19.0.6 / 19.1.7 / 19.2.6 |

## 破壊的変更・移行ガイド

破壊的変更はなし。パッチバージョンのアップグレードのみで対応可能。

**対応手順:**
1. `next` パッケージを 15.5.18 または 16.2.6 にアップデート
2. `react-server-dom-*` パッケージが使用されている場合は対応バージョンにアップデート
3. Cloudflare / Netlify 等の CDN を利用している場合、各プロバイダーの WAF ルール更新を確認

**ミドルウェアに認可ロジックを依存させている場合の注意:**
- ミドルウェアバイパスの脆弱性が複数含まれるため、ミドルウェアのみでアクセス制御を行っている場合は特に速やかなアップグレードが必要
- 長期的にはミドルウェアだけでなくサーバーサイドでの多層防御を検討

## 今後の注目点

- Next.js 13〜14.x はサポート終了に近づいており、今回の修正も 15.x / 16.x のみ。レガシーバージョンからの移行を計画すべき
- React Server Components の成熟に伴い、サーバーサイド固有の攻撃ベクトル（DoS、SSRF）に対するセキュリティ意識の向上が必要
- Cloudflare、Netlify 等の主要 CDN プロバイダーが WAF ルールで即座に対応しており、CDN レベルでの緩和も有効
