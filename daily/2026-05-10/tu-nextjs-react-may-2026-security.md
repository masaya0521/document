# Next.js / React 2026年5月セキュリティ一括修正

- **日付**: 2026-05-10
- **カテゴリ**: Frontend / Backend (Web Framework)
- **ソース**: [Vercel changelog](https://vercel.com/changelog/next-js-may-2026-security-release), [Cloudflare changelog](https://developers.cloudflare.com/changelog/post/2026-05-06-react-nextjs-vulnerabilities/), [Netlify changelog](https://www.netlify.com/changelog/2026-05-08-react-nextjs-security-vulnerabilities/), [ZeroPath blog](https://zeropath.com/blog/cve-2026-23870-react-server-components-dos)

## 概要

Vercel と React チームは 5/6 〜 5/7 にかけて Next.js / React Server Components の脆弱性 12 件（一部報道では 13 件）を一斉公表・修正した。React Server Components 由来の DoS（CVE-2026-23870）が 1 件、残りは Next.js のミドルウェア / プロキシバイパス、XSS、SSRF、キャッシュポイズニング、DoS など多岐に渡る。App Router を使用している場合は影響範囲が広く、即時アップグレードが推奨される。

修正版は Next.js 15.5.18 / 16.2.6、React 側は `react-server-dom-parcel` / `react-server-dom-webpack` / `react-server-dom-turbopack` の 19.0.6 / 19.1.7 / 19.2.6。

## 主な変更点

### CVE-2026-23870: React Server Components の DoS

- **影響**: React 19.x、および Next.js App Router を使う 13.x / 14.x / 15.x / 16.x すべて
- **原因**: React の "Flight" プロトコルのデシリアライズが、入力ペイロードに対する構造的・型的制約を十分に強制していなかった
- **挙動**: Server Function エンドポイントに対して特殊に構築された HTTP リクエストを送ると、デシリアライズ時に過剰な CPU を消費し DoS を誘発できる

### Next.js 11 件の脆弱性カテゴリ

- ミドルウェア / プロキシバイパス
- SSRF（Server-Side Request Forgery）
- キャッシュポイズニング
- XSS
- DoS

詳細な個別 CVE 番号は Vercel の changelog および GitHub Security Advisory に列挙されている。

### プラットフォーム / アダプタ側の対応

- **Cloudflare**: WAF Managed Rules を更新し、影響を受けるパターンをブロック。OpenNext の Cloudflare アダプタも追従更新
- **Netlify**: Next.js Runtime をアップデートし、ホスト側で攻撃ベクタの一部を緩和
- **OpenNext / SST 等のセルフホスト系**: 各アダプタの最新版に追従してデプロイ環境ごと更新が必要

## 破壊的変更・移行ガイド

破壊的変更は基本的になし。マイナー/パッチアップグレード扱いで、依存パッケージの整合のみ揃えれば良い。

### アップグレード手順

```bash
# Next.js (App Router を利用しているプロジェクトすべて)
pnpm add next@16.2.6
# あるいは 15 系のまま運用する場合
pnpm add next@15.5.18

# React Server Components のバンドラパッケージは利用ビルド系統に合わせて
pnpm add react-server-dom-webpack@19.2.6
pnpm add react-server-dom-turbopack@19.2.6
pnpm add react-server-dom-parcel@19.2.6
```

App Router 利用プロジェクトでは Server Function エンドポイントの呼び出し経路を一通りリグレッションテストすること。Server Actions / `use server` 関数を多用するアプリは特に重点確認が必要。

### 一時緩和策

完全な緩和はパッチ適用のみ。とはいえ即時パッチが難しい環境では:

- Cloudflare WAF / Vercel Firewall / 自前の WAF で `multipart/form-data` / RSC payload に対する size limit / rate limit を強化
- Server Actions エンドポイントへの直接アクセスを認証付き経路に限定

## 今後の注目点

- React チームは Flight プロトコルの payload バリデーションを構造化する方向で再設計を進めると見られる。今後マイナーリリースで段階的に強化される可能性
- 過去 1 年で Next.js / React Server Components の重大 CVE が高頻度で出ている（2025-12 の CVE-2025-66478、2026-01 の DoS、本件）。RSC は表面積が広く、自前で薄くラップしている SaaS / プラットフォーム側の追従コストが高まっている
- セルフホストのプロジェクトはリリース監視と通知設定（GitHub の security advisory subscription、Dependabot / Renovate のセキュリティアラート優先化）を整える時期
