# Svelte / SvelteKit — June 2026

- **日付**: 2026-06-21
- **カテゴリ**: Frontend
- **ソース**: [What's new in Svelte: June 2026](https://svelte.dev/blog/whats-new-in-svelte-june-2026), [sveltejs/svelte Releases](https://github.com/sveltejs/svelte/releases)

## 概要

2026 年 6 月の Svelte / SvelteKit アップデートは、**Remote Functions（リモート関数）** の API 刷新が中心。長寿命なサーバーサブスクリプションを扱う `query.live()` の async-iterable 化、イベントハンドラやモジュールスコープでの query の await 対応など、リアルタイム/非同期データ処理の取り回しが大きく改善された。一方で `.run()` の廃止や enhance コールバックの引数変更など、**破壊的変更**を複数含むため、Remote Functions を利用しているプロジェクトは移行が必要。

- **SvelteKit**: 2.57.0〜2.61.0
- **Svelte**: 5.56.0
- **Language Tools**: 0.18.0+（TypeScript 6 対応）

## 主な変更点

### `query.live()` API（2.59.0 で experimental、2.61.0 で async）
長寿命なサーバーサブスクリプションが async iteration をサポートし、リアルタイムデータのワークフローを書きやすくなった。

### Remote Functions の改善
- query をイベントハンドラ・非同期コールバック・モジュールスコープで **await** できるようになり、リアクティブ/非リアクティブ両方の consumer でキャッシュの dedup を共有（2.61.0）。
- `query.batch()` によるバッチ処理の inspection に対応（2.59.0）。
- `requested()` が `limit` 引数を必須化し、`{ arg, query }` のエントリを返すよう変更（2.58.0）。

### フォーム処理の強化
- remote form の `submit()` がバリデーション状態を示す boolean を返すように（2.57.0）。
- `submit` / `hidden` フィールドが boolean・number をそのまま受け取れる（2.60.0）。
- 読まれなかった remote form のバリデーションエラーを警告し、UX の見落としを早期検出（2.60.0）。

### その他
- テンプレートのマークアップ内で直接宣言が可能に（5.56.0）。
- language-tools エコシステム全体で TypeScript 6.0 をサポート。
- Svelte MCP の stdio モードでファイル操作のラウンドトリップを削減。

## 破壊的変更・移行ガイド

1. **`.run()` の廃止（2.61.0）**
   - remote query から `.run()` が削除された。すべてのコンテキストで `await query()` を直接使う形に書き換える。
   ```js
   // Before
   const data = await myQuery.run();
   // After
   const data = await myQuery();
   ```

2. **`requested()` の構造変更（2.58.0）**
   - `limit` が必須になり、返り値のオブジェクト形状が変化（`{ arg, query }` エントリを yield）。

3. **enhance コールバックの引数変更（2.61.0）**
   - これまでの `{ form, data, submit }` オブジェクトではなく、**form remote function のインスタンスのコピー**を受け取るようになった。
   - form インスタンスはプログラム的な `submit()` API を公開する。

## 今後の注目点

- Remote Functions は依然として API が活発に変化している領域。`query.live()` の async 安定化を受け、リアルタイム機能の実装パターンが固まっていくか要ウォッチ。
- TypeScript 6.0 対応が language-tools 全体に行き渡ったことで、型まわりの開発体験向上が見込まれる。
