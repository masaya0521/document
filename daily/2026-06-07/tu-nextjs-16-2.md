# Next.js — 16.2

- **日付**: 2026-06-07
- **カテゴリ**: Frontend
- **ソース**: [Next.js 16.2 Blog](https://nextjs.org/blog/next-16-2), [Next.js Changelog](https://next-changelog.vercel.app/), [Upgrading: Version 16](https://nextjs.org/docs/app/guides/upgrading/version-16)

## 概要

Next.js 16.2 は、新たに **Adapters** API を導入し、デプロイ先プラットフォームごとのビルド/ランタイム挙動を拡張できるようにした、Next.js 16 系のマイナーリリース。開発体験とランタイム性能の両面に大きく踏み込んでおり、`next dev` の起動が約 400% 高速化、レンダリングが約 50% 高速化、200 以上のバグ修正を含む。Turbopack はさらに成熟し、サーバーサイドの細粒度ホットリロード（Server Fast Refresh）や Subresource Integrity（SRI）対応が加わった。

2026年6月時点では、16.2 系に対してドキュメント修正・dev モードのハイドレーション修正・キャッシュタグエンコーディング改善・Server Action / middleware 修正・Turbopack HMR 修正などの backport が継続して取り込まれている。

## 主な変更点

### Adapters
- デプロイ先プラットフォーム向けに、ビルド出力やランタイムの挙動をフックできる Adapter API を追加。プラットフォーム差異の吸収をフレームワーク標準の仕組みとして提供する。

### パフォーマンス
- **Faster Time-to-URL**: `next dev` の起動が約 400% 高速化。
- **Faster Rendering**: レンダリングが約 50% 高速化。
- **新デフォルト 500 ページ**: 組み込みの 500 エラーページを刷新。

### Turbopack
- **Server Fast Refresh**: サーバーサイドコードの細粒度なホットリロード。
- **Web Worker Origin**: Worker 内での WASM ライブラリ利用サポートを拡充。
- **SRI 対応**: JavaScript ファイルに対する Subresource Integrity をサポート。
- ビルドの高速化と多数の修正。

### AI 関連
- AI 対応の `create-next-app`（AI-ready）。
- ブラウザログのフォワーディング。
- dev サーバーのロックファイルハンドリング。
- 実験的な **Agent DevTools**。

## 破壊的変更・移行ガイド

- 16.2 自体はマイナーリリースであり、16 系内での移行は基本的に追従が中心。16.x への更新は `npx @next/codemod@canary upgrade latest` などのコーデモッドを利用すると差分対応が容易。
- メジャーである Next.js 16 へ未移行の場合は、[Version 16 へのアップグレードガイド](https://nextjs.org/docs/app/guides/upgrading/version-16) に従い、非同期 API（`cookies()` / `headers()` / `params` 等）や caching 既定値の変更点を確認すること。

## 今後の注目点

- Adapters エコシステムが各ホスティングプラットフォームでどこまで採用されるか。
- Turbopack の安定版デフォルト化に向けた完成度（Server Fast Refresh / SRI の実運用評価）。
- Agent DevTools をはじめとする AI 駆動開発フローのフレームワーク統合の進展。
