# Next.js + React — 2026 年 5 月セキュリティリリース

- **日付**: 2026-05-14
- **カテゴリ**: Frontend
- **ソース**:
  - [Vercel: Next.js May 2026 security release](https://vercel.com/changelog/next-js-may-2026-security-release)
  - [Vercel: Summary of CVE-2026-23869](https://vercel.com/changelog/summary-of-cve-2026-23869)
  - [Netlify changelog](https://www.netlify.com/changelog/2026-05-08-react-nextjs-security-vulnerabilities/)
  - [Cloudflare: WAF and framework adapter mitigations](https://developers.cloudflare.com/changelog/post/2026-05-06-react-nextjs-vulnerabilities/)
  - [Akamai: CVE-2026-23864](https://www.akamai.com/blog/security-research/cve-2026-23864-react-nextjs-denial-of-service)
  - [ZeroPath: CVE-2026-23870 Brief Summary](https://zeropath.com/blog/cve-2026-23870-react-server-components-dos)

## 概要

Next.js と React の両チームによる協調セキュリティリリースで、5/6 に 12 件、5/7 に追加 1 件、計 13 件の脆弱性アドバイザリが一度に公開された。Next.js 側は 11 件、React 側は React Server Components (RSC) に絡む 1 件で、内訳は DoS・ミドルウェア / プロキシ経由の認証バイパス・SSRF・キャッシュポイズニング・XSS など、いずれも実プロダクションのアプリにそのまま刺さるカテゴリ。

修正は **Next.js 15.5.18 と 16.2.6**、および React の `react-server-dom-parcel` / `react-server-dom-webpack` / `react-server-dom-turbopack` の **19.0.6 / 19.1.7 / 19.2.6** に入っている。15.x・16.x の **これより前のマイナーにはバックポートされない** ため、たとえば 15.4 系を使っているプロジェクトは 15.5 系へマイナーアップが必要になる点が大きな運用ポイント。

## 主な変更点

13 件の修正のうち、特に影響が広いものを抜粋する。

- **CVE-2026-23870 — React Server Components の DoS**
  App Router の Server Function エンドポイントに細工した HTTP リクエストを送ると、デシリアライズ処理で CPU を食い潰せる。Next.js の App Router を使う 13.x / 14.x / 15.x / 16.x がすべて対象。
- **App Router segment-prefetch URL によるミドルウェア / 認可バイパス**
  プリフェッチ用 URL を経由して、本来ミドルウェアで止めるべきリクエストが認可レイヤを素通りするパターン。
- **Pages Router の i18n 既定ロケールパスを使った認可バイパス**
  既定ロケールへのリクエストでパス比較を回避できるケース。Pages Router 側で `i18n` を使っているサイトに影響。
- **SSRF (WebSocket upgrade リクエスト)**
  self-host の Node.js デプロイ環境で、WebSocket Upgrade を細工した内部リクエストに変換されてしまう。Vercel ホスティングはこの面では影響を受けにくいが、自前ホストは対象。
- **RSC レスポンスのキャッシュポイズニング**
  RSC のレスポンスがキャッシュ層に汚染されて、別ユーザに別ユーザ用の RSC ペイロードが配られる経路。
- **CSP nonce を使う App Router での XSS**
  CSP の `nonce` を使っていても、特定の経路ではバイパスできるという報告。

## 破壊的変更・移行ガイド

挙動上の破壊的変更は実装上限定的だが、運用としては以下を踏む必要がある。

1. 利用中の Next.js を **15.5.18 もしくは 16.2.6** に上げる。15.5 / 16.2 より古いマイナーを使っている場合はまずマイナーアップを行う。
2. App Router で RSC を使っている場合は **React 19 系も対応バージョンへ**。具体的には `react-server-dom-*` を 19.0.6 / 19.1.7 / 19.2.6 のいずれかに揃える。
3. self-host (Node.js / Bun 等) 環境では、SSRF 系の修正は **adapter / runtime のアップデートも合わせて必要** になる場合がある。Cloudflare・Netlify などはホスティング側で WAF / アダプタ側のミティゲーションを実施しているので、ホスティング各社の changelog も合わせて参照。
4. すぐにアップグレードできない場合の緩和策として、WAF ルール (Cloudflare 等) と、ミドルウェア / 認可レイヤを **URL パス比較だけに頼らない実装**（実 URL 正規化、HTTP メソッド・ヘッダの追加検証）に寄せる。

## 今後の注目点

- **「マイナーは最新を使う」運用の徹底**。今回のように patch 配布が "patched minor" 限定になる方針は今後も続く可能性が高い。15.4 → 15.5、16.1 → 16.2 のような小幅マイナーアップを止めないこと。
- **App Router の URL ベース認可は要見直し**。今回のミドルウェアバイパス系は、認可をパス比較・正規表現に強く寄せた実装で被害が大きい。Server Action / Route Handler 側でユーザ単位の権限チェックを必ず重ねる設計に揃えておきたい。
- **RSC を介したキャッシュ / SSRF の流れ**は、今後も周辺パッケージ（adapter、ホスティング層、CDN）と組み合わせて新しい攻撃面を生む見込み。WAF ベンダ・ホスティング各社の更新も継続して追う。
