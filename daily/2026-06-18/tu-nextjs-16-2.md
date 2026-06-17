# Next.js 16.2 — Cache Components と use cache

- **日付**: 2026-06-18
- **カテゴリ**: Frontend
- **ソース**: [Next.js 16.2 公式ブログ](https://nextjs.org/blog/next-16-2), [GitHub Releases](https://github.com/vercel/next.js/releases)

## 概要

Next.js 16.2 は、16 系で導入された **Cache Components** を中心に、キャッシュモデル・開発体験・ビルド拡張性を強化したリリース。キャッシュが従来の「暗黙的・グローバル」から「明示的・コンポーザブル」へと設計転換した点が最大の特徴で、`use cache` ディレクティブを file / function / component の 3 スコープで適用できる。あわせて dev サーバ起動が 16.1 比で約 87%（約 4 倍）高速化するなど、Turbopack を軸にしたパフォーマンス改善も大きい。

## 主な変更点

- **Cache Components（PPR + use cache）**: Partial Pre-Rendering を活かした新しいプログラミングモデル。キャッシュ対象を明示的に宣言することで、即時ナビゲーションとコンポーザブルなキャッシュ戦略を両立する。
  - `use cache` は **ファイル単位 / 関数単位 / コンポーネント単位** の 3 スコープで適用可能。
- **パフォーマンス**: dev サーバ起動が 16.1 比で約 87% 高速化。OG 画像生成の `ImageResponse` API が 2〜20x 高速化。
- **Build Adapters の安定化**: `adapterPath` 設定が alpha から stable に昇格。ビルド成果物のパッケージ方法をホスティングプラットフォーム向けにカスタマイズできる。ビルド完了後に独自ロジック（プラットフォーム固有のマニフェスト生成、アセットアップロード等）を走らせる `onBuildComplete` フックが新規追加。
- **AI / DX 改善**: AI-ready な `create-next-app`、ブラウザログのフォワーディング、dev サーバのロックファイル処理、実験的な Agent DevTools。
- **16.2 バックポート**: ドキュメント更新、ハイドレーション・ルータ修正、キャッシュタグのエンコーディング改善、Server Action / middleware 修正、Turbopack 変更、FormData ハンドリング改善など安定化フィックスを含む。

## 破壊的変更・移行ガイド

- Cache Components はキャッシュを「明示的に宣言する」モデルへ移行するため、既存アプリは **キャッシュ箇所の棚卸し（audit）が必要**。これまで暗黙のグローバルキャッシュに依存していた挙動は、`use cache` を明示しない限りキャッシュされなくなる前提で見直すこと。
- `unstable_cache` から `use cache` への移行が推奨される流れ。両者の使い分け（スコープ、再検証タグの扱い）を確認した上で段階的に置き換えるのが安全。

## 今後の注目点

- Cache Components / PPR が安定版として定着し、App Router のデフォルトのキャッシュ戦略としてどこまで普及するか。
- Turbopack の dev / build 双方での高速化が、Webpack 系ワークフローからの移行をさらに後押しするか。
- Build Adapters と `onBuildComplete` により、Vercel 以外のホスティングプラットフォームでの一級サポートが広がるか。
