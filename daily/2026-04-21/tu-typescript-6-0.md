# TypeScript 6.0 — JavaScript ベース最後のメジャーリリース

- **日付**: 2026-04-21
- **カテゴリ**: Language
- **ソース**: [Announcing TypeScript 6.0](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [TypeScript 6.0 Ships as Final JavaScript-Based Release (Visual Studio Magazine)](https://visualstudiomagazine.com/articles/2026/03/23/typescript-6-0-ships-as-final-javascript-based-release-clears-path-for-go-native-7-0.aspx), [Handbook Release Notes](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-6-0.html)

## 概要

TypeScript 6.0 は 2026-03-23 にリリースされた、従来の JavaScript 実装 (`tsc`) をベースとした最後のメジャーバージョン。次期 7.0（コードネーム "Corsa"）は Go で書き直された新実装になる予定で、6.0 はその移行に備えるための「橋渡し」リリースと位置づけられている。ロードマップ上は 7.0 で 5-10x のビルド高速化、エディタ起動 8x、メモリ使用量 50% 削減が見込まれており、2026 年夏〜年末のリリースが目標とされている。

このため 6.0 自体の新機能は最小限に抑えられているが、7.0 で挙動が変わる箇所を「今のうちに気付けるようにする」ための機能追加と、既に非推奨だった構文の正式廃止が中心になっている。

## 主な変更点

### 1. `--stableTypeOrdering` フラグの導入

TypeScript 7.0 は並列型チェックのため、内部型 ID を決定論的にソートする新アルゴリズムを採用する。これにより宣言ファイル出力中の Union の順序が 6.0 と 7.0 で変わる可能性がある。

`--stableTypeOrdering` を有効にすると、6.0 のコンパイラが 7.0 と同じ順序で型を出力する。これによって 7.0 移行前に diff を取って差異を検出できる。

- 恒久設定ではなく、**移行診断用**として使うことが推奨されている
- コードベース次第で型チェックが最大 25% 遅くなる可能性があるため、CI / 開発時に常用しない

### 2. ジェネリック JSX 式での型チェック強化

ジェネリック呼び出し、特にジェネリック JSX 式での関数式の型チェック挙動が調整され、より多くの既存バグを検出するようになった。既存コードでビルドエラーが新たに発生し得るため、アップグレード時の主要な破壊的変更のひとつ。

### 3. 動的 `import()` での `assert` 構文の非推奨化

- 既存の静的 `import ... assert { type: "json" }` の非推奨は 5.3 で導入済み
- 6.0 では動的 `import(..., { assert: { type: "json" } })` も非推奨になった

```ts
// 非推奨
const mod = await import("./data.json", { assert: { type: "json" } });

// 推奨 (import attributes 提案ベース)
const mod = await import("./data.json", { with: { type: "json" } });
```

`assert` → `with` は単なる改名ではなく、**読み込み挙動に影響し得るセマンティクス**を持つ `with` への移行であり、TC39 の `import attributes` 提案に沿った変更。

### 4. DOM 型の更新

現行 Web 標準を反映し、Temporal API 周辺の型も調整された。

## 破壊的変更・移行ガイド

| 変更 | 影響範囲 | 対応 |
|---|---|---|
| 動的 `import()` の `assert` 非推奨 | JSON/CSS モジュールのロードコード | `assert` → `with` に置換 |
| ジェネリック JSX 型チェック強化 | React 等のジェネリックコンポーネント呼び出し | 型エラーを修正、多くは実際のバグ |
| 型 ID 順序が 7.0 と異なり得る | `.d.ts` を配布するライブラリ | `--stableTypeOrdering` で差分を事前確認 |
| DOM / Temporal 型更新 | DOM API を広く使うコード | 型エラーが出た箇所を順次対応 |

既存プロジェクトの移行は、まず 6.0 にアップグレードし、`--stableTypeOrdering` を一時的に有効化して 7.0 で壊れる箇所を洗い出す、という二段階戦略が推奨されている。

## 今後の注目点

- **TypeScript 7.0 (Corsa)**: Go 実装、決定論的型順序、並列型チェック。2026 年中後半のリリースが目標
- **tsgo**: 7.0 のコンパイラ部分だけを先行提供する形態も検討されている。CI 組み込み時の互換性検証が鍵
- **エコシステム対応**: 型生成を行うツール（tsup, tsx, Vite の `vite-plugin-dts` 等）が 7.0 の新しい型 ID 順序にどう追従するか
- **既存コードの移行難易度**: メジャーバージョン番号は飛ぶが、7.0 は「書き直しリリース」のため、API・構文レベルでの破壊的変更は 6.0 ほど多くない可能性が高い
