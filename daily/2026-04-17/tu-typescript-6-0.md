# TypeScript 6.0 — JS 実装時代の最終リリースと 7.0（Go 実装）への橋渡し

- **日付**: 2026-04-17（元リリース日: 2026-03-23）
- **カテゴリ**: Language
- **ソース**: [Announcing TypeScript 6.0 — Microsoft Dev Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [Announcing TypeScript 6.0 RC](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [Visual Studio Magazine — TypeScript 6.0 Ships](https://visualstudiomagazine.com/articles/2026/03/23/typescript-6-0-ships-as-final-javascript-based-release-clears-path-for-go-native-7-0.aspx)

## 概要

TypeScript 6.0 は、現行の JavaScript 実装で提供される最後のメジャーリリースとして 2026 年 3 月 23 日にリリースされた。機能追加よりも、Go 言語で書き直された 7.0 系（Project Corsa）への移行を円滑にすることが主眼で、多数のオプションが廃止または非推奨化されている。5.x 系からの後方互換は保たれているが、`tsconfig.json` のデフォルト値は 7.0 を見据えて大きく変わる。

## 主な変更点

### 型推論・新機能

- `this` を使わないメソッド構文の関数にも、アロー関数と同様の contextual typing が適用されるようになり、ジェネリック呼び出しでの推論が一貫した挙動に。
- サブパスインポート（`#/...`、Node.js 20+）をサポート。
- `--moduleResolution bundler` と `--module commonjs` の組み合わせが可能に。
- ES2025 API サポート: `RegExp.escape`、Temporal API、Map/WeakMap の `upsert` など。
- `--stableTypeOrdering` フラグで、6.0 の出力型の並び順を 7.0 と揃えられる（最大 25% の性能コスト）。

### コード例: `this`なしメソッドの contextual typing

```ts
// 5.x では <T> の推論が通らないことがあった
declare function run<T>(cb: { handle(value: T): void }): void;

run({
  handle(value) {
    // 6.0 からは value の型が正しく推論される
  },
});
```

## 破壊的変更・移行ガイド

### デフォルト値の変更

| オプション | 旧デフォルト | 新デフォルト |
|-----------|------------|------------|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | 固定 | `ES2025`（最新年版） |
| `rootDir` | 推測 | `tsconfig.json` のディレクトリ |
| `types` | 自動 | `[]` |

既存プロジェクトを 6.0 に上げる際は、必要な `types: ["node"]` や `module` を明示的に書き戻す必要がある。

### 廃止（7.0 で完全削除）

- `target: es5`
- `baseUrl`（モジュール解決ルート用途）
- `--module amd` / `umd` / `systemjs`
- `--moduleResolution node`（node10）/ `classic`
- `outFile`（バンドラー推奨）

6.0 では `"ignoreDeprecations": "6.0"` で警告を抑制できるが、7.0 ではオプション自体が削除されるため、6.0 運用中に段階的な対応が求められる。

### 推奨移行ステップ

1. 6.0 に上げて deprecation 警告を確認。
2. 廃止予定オプションを差し替え（AMD/UMD 等 → ESM/CJS、`baseUrl` → `paths`、`outFile` → バンドラー）。
3. デフォルト変化を吸収するため、既存の暗黙設定を明示化。
4. `--stableTypeOrdering` を有効にして 7.0 互換の出力を試す。

## 今後の注目点

- **TypeScript 7.0 (Project Corsa)**: Go 実装で、コンパイル 5-10 倍、エディタ起動 ~8 倍、メモリ 50% 削減を謳う。2026 年夏〜秋リリース予定。VS Code 1.107 には experimental の native language server 統合が既に入っており、大規模コードベースでの採用実績も報告されている。
- **型推論の互換性**: 6.0 と 7.0 で型表示の並び順が変わる場合があるため、型スナップショットテストに依存するプロジェクトは `--stableTypeOrdering` の利用を検討する価値がある。
- **エコシステム追従**: ts-node / tsx / ts-jest / vitest など、コンパイラの内部 API に依存するツールは 7.0 で再調整が必要。移行前に上流の対応状況を確認したい。
