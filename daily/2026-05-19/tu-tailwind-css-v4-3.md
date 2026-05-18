# Tailwind CSS v4.3.0 — スクロールバーユーティリティとコンテナサイズクエリ

- **日付**: 2026-05-12
- **カテゴリ**: Frontend
- **ソース**:
  - [Tailwind CSS Blog: v4.3](https://tailwindcss.com/blog/tailwindcss-v4-3)
  - [Laravel News: Scrollbar Styling and Container Size Utilities](https://laravel-news.com/scrollbar-styling-and-container-size-utilities-in-tailwind-css-v430)
  - [GitHub Releases: tailwindlabs/tailwindcss](https://github.com/tailwindlabs/tailwindcss/releases)

## 概要

Tailwind CSS v4.3.0 が 2026-05-12 にリリース。スクロールバーを CSS だけで一級ユーティリティから制御できるようになり、コンテナクエリには高さに反応する `@container-size` が追加された。さらに mauve / olive / mist / taupe の 4 つのニュートラル系カラーパレットと、Next.js 等で効果が大きい webpack 専用プラグインが同梱されている。破壊的変更は文書化されていない。

これまで PostCSS / browser ベンダーごとに半端な API を使い分けていた領域（特にスクロールバー）が、`scrollbar-thin scrollbar-thumb-sky-700` のような形で他のユーティリティと自然に並ぶようになった点が実務面で大きい。

## 主な変更点

### スクロールバーユーティリティ

3 系統のユーティリティ:

- **幅**: `scrollbar-auto` / `scrollbar-thin` / `scrollbar-none`（`scrollbar-width` プロパティ）
- **色**: `scrollbar-thumb-*` / `scrollbar-track-*`（フルカラーパレット + opacity モディファイア対応）
- **gutter**: `scrollbar-gutter-auto` / `scrollbar-gutter-stable` / `scrollbar-gutter-both`（スクロールバー出現時のレイアウトシフト防止）

```html
<div class="scrollbar-thin scrollbar-thumb-sky-700 scrollbar-track-sky-100 overflow-auto">
  ...
</div>
```

### 新カラーパレット

`mauve` / `olive` / `mist` / `taupe` の 4 種、いずれも 50〜950 のシェードを持つニュートラル寄りのトーン。既存の `gray` / `zinc` / `neutral` / `stone` / `slate` よりわずかにキャラクターを持たせたい場面向け。

### コンテナクエリ強化

`@container-size` ユーティリティで size container を作成可能に。これまで `inline-size` 軸だけだったコンテナクエリが、`cqb` / `cqh` 単位で高さにも反応するようになる。レスポンシブな縦比例 UI が書きやすくなった。

### その他のユーティリティ

| 機能 | 内容 |
|------|------|
| `font-features-*` | `font-feature-settings` を制御。tabular numbers 等の OpenType 機能をクラスで指定 |
| `zoom-*` | CSS `zoom` プロパティ。任意値・CSS 変数対応 |
| `tab-*` | `tab-size` でタブ幅を制御 |
| `@tailwindcss/webpack` | webpack 専用ローダーで、従来の PostCSS 経由比 **2.17x 高速** な再ビルド |

### プラグイン開発の改善

`@variant` でスタック・複合バリアントを記述できる:

```css
/* スタック（連結）バリアント */
@variant hover:focus { ... }

/* 複合（OR）バリアント */
@variant hover, focus { ... }
```

functional utility にデフォルト値 `--default(4)` も書けるようになり、プラグイン作成時の堅牢性が上がった。

## 破壊的変更・移行ガイド

リリースノート上、**破壊的変更の記載はなし**。`@tailwindcss/vite` および `@tailwindcss/postcss` ユーザーはバージョンを上げるだけで取り込める。webpack ユーザーは新パッケージ `@tailwindcss/webpack` の導入で大幅な速度改善が見込めるため、Next.js / CRA 系プロジェクトでは置き換えを検討する価値がある。

## 今後の注目点

- **スクロールバー API のブラウザ実装差**: Firefox / Chromium / Safari でカバレッジが異なる領域。Tailwind 側で吸収されているが、深い指定では結局ブラウザ依存になる点に注意
- **コンテナクエリのデザイン採用**: `@container-size` で高さに反応する UI が書けるようになり、これまで viewport units / JS で対処していたパターンが CSS だけで完結する可能性
- **webpack plugin の Next.js 採用**: Next.js のビルド時間短縮にどこまで効くかは要計測。大型プロジェクトでの数値共有が出てくるはず
- **Vite 8（Rolldown）との組み合わせ**: 2026-03 リリースの Vite 8 と組み合わせると、フロントエンドのビルド時間は数十秒台から一桁秒台へ圧縮される事例が増えそう
