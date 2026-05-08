# React / Next.js — RSC 関連脆弱性パッチリリース（2026-05-06）

- **日付**: 2026-05-06
- **カテゴリ**: Frontend
- **ソース**: [Cloudflare Changelog — WAF and framework adapter mitigations](https://developers.cloudflare.com/changelog/post/2026-05-06-react-nextjs-vulnerabilities/), [React Versions](https://react.dev/versions), [React Blog — December 2025 RSC Security](https://react.dev/blog/2025/12/11/denial-of-service-and-source-code-exposure-in-react-server-components)

## 概要

2026-05-06、React Server Components（RSC）周りで新たに開示された DoS 系の脆弱性に対するパッチが公開された。React 19 系は 3 ライン同時にメンテリリースが行われ、`react-server-dom-webpack` / `react-server-dom-parcel` / `react-server-dom-turbopack` の `19.0.6` / `19.1.7` / `19.2.6` でパッチが適用されている。Next.js 側は `15.5.16` と `16.2.5` がパッチ版として配布されている。

Cloudflare は同日に WAF マネージドルールとフレームワーク用アダプタを更新し、フレームワーク側のアップデートが追いつかない環境でもネットワーク層で緩和策を提供できるようにした。RSC を本番投入しているチームにとっては、フレームワーク・依存・エッジの 3 段で対処が必要なケース。

## 主な変更点

### パッチ対象

- React 系（react-server-dom-* パッケージ）
  - `19.0.6`
  - `19.1.7`
  - `19.2.6`
- Next.js 系
  - `15.5.16`
  - `16.2.5`

### Cloudflare 側の対応

- WAF マネージドルールに今回開示された RSC DoS 系シグネチャを追加。
- Workers の Next.js / React Router 用フレームワークアダプタを更新。
- 既存の RSC 系 CVE（CVE-2025-55184、CVE-2026-23864 など）向けに展開済みのルールが、今回の DoS 脆弱性にも一部カバレッジを提供している。

### 背景となる過去 CVE

| CVE | 内容 |
|-----|------|
| CVE-2025-55182 | React Server Components の RCE 脆弱性 |
| CVE-2025-55183 / 55184 | React / Next.js の DoS（RSC ペイロード経由） |
| CVE-2026-23864 | React / Next.js のメモリ枯渇による DoS（CVSS 7.5） |

今回の 5 月パッチはこれらの一連の流れに連なるもので、RSC レンダリングパイプライン上の入力バリデーションとサイズ制限が継続的に強化されている。

## 破壊的変更・移行ガイド

破壊的変更はなく、すべてセキュリティ修正を含むパッチリリース。以下の優先順で対処を推奨。

1. **React のバージョンに合わせて upgrade**
   - 19.0 系 → `19.0.6`
   - 19.1 系 → `19.1.7`
   - 19.2 系 → `19.2.6`
   - `react-server-dom-webpack` / `react-server-dom-parcel` / `react-server-dom-turbopack` を React 本体と同じバージョンに揃える。
2. **Next.js のバージョンに合わせて upgrade**
   - 15 系 → `15.5.16`
   - 16 系 → `16.2.5`
3. **エッジ層の対策を確認**
   - Cloudflare 利用なら WAF マネージドルールが最新で適用されているか確認。
   - 他 CDN / WAF 利用時は同様の RSC ペイロードサイズ制限ルールを検討。
4. **依存解析**
   - サードパーティ製 React フレームワーク（Remix / React Router v7 など）も RSC 機能を有効化している場合は、本体側の対応状況を確認。

RSC を使っていない場合でも、`react-dom/server` 経由で SSR ペイロードに似たパスが影響を受けるかは確認しておくと安心。

## 今後の注目点

- 2025-12 → 2026-01 → 2026-05 と続いている RSC 系 CVE のラッシュは、RSC が本番投入されたフェーズ特有の "新しいアタックサーフェスが洗い出されている期間" と捉えられる。攻撃面の体系化（OWASP 等での整理）が進むかどうか。
- フレームワーク層（Next.js）と React 本体・`react-server-dom-*` パッケージの 3 つを同時にバージョン管理する構造が常態化しているため、社内の dependency management に「RSC パッケージの揃え方」を明記しておくと事故が減る。
- Cloudflare のように WAF 側で同期して緩和策を出す動きは、エッジ + フレームワーク の協調 defense の好例。AWS WAF / Akamai 側のシグネチャ更新ペースも要観察。
- RSC を採用するチームは、CVE を踏んで急ぐより、定期的なアップグレード運用（少なくとも月次でのパッチ適用）を体制化しておくことが推奨される。
