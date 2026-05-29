# SvelteKit — 2026年5月アップデート（2.56.0 / 2.57.0）

- **日付**: 2026-05
- **カテゴリ**: Frontend
- **ソース**: [What's new in Svelte: May 2026](https://svelte.dev/blog/whats-new-in-svelte-may-2026), [sveltejs/kit Releases](https://github.com/sveltejs/kit/releases)

## 概要

2026年5月の Svelte エコシステムは、SvelteKit の remote functions の継続的な強化、TypeScript 6.0 対応、そして Svelte CLI（`sv`）でのコミュニティ add-on の実験的提供が中心となった。remote functions は SvelteKit の新しいデータ取得・ミューテーションの仕組みで、今月は transport 層・フォーム連携の両面で実用性が高まった。

## 主な変更点

### TypeScript 6.0 対応（2.56.0）
- TypeScript 6.0 をサポートし、最新の言語機能が利用可能に。

### フォーム機能の改善
- **`field.as(type, value)`**（2.56.0）: フォームフィールドに初期値を指定できるようになり、事前入力フォームのボイラープレートを削減。
- **送信妥当性の boolean 返却**（2.57.0）: enhanced form の remote function で、フォーム送信が妥当性を示す boolean を返すように。

### Remote Functions の拡張
- transport が `hydratable` を使用するようになり、クエリ結果でより豊富なデータ型（リッチな型）をサポート（2.56.0）。
- `run()` メソッドを追加し、レンダリング外でのクエリ待機を禁止することで誤用を防止。
- キャッシュキーをソートしてキャッシングの安定性を向上。

### Svelte CLI・開発ツール
- `sv` コマンドでコミュニティ add-on を実験的機能として提供開始。
- `sv` と `sv-utils` を分離し、公開 API をより明確化。
- Vitest v3 検出の信頼性を向上。
- `svelte/motion` から `TweenOptions` / `SpringOptions` 型をエクスポート。

## 破壊的変更・移行ガイド

- 今回はマイナー／パッチ範囲のリリースで、破壊的変更は告知されていない。TypeScript 6.0 を採用済みのプロジェクトは 2.56.0 以降へ更新することで型エラーを回避できる。

## 今後の注目点

- remote functions は SvelteKit のデータ層の今後を担う機能で、transport の hydratable 化により tRPC 的な型安全な RPC 体験に近づいている。今後の安定化と採用事例に注目。
- `sv` CLI のコミュニティ add-on 実験提供は、エコシステム拡張（認証・DB・デプロイ等のセットアップ自動化）の入り口となる。
