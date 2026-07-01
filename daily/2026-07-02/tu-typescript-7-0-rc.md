# TypeScript — 7.0 RC（Go ネイティブコンパイラ）

- **日付**: 2026-06-18（RC 公開）
- **カテゴリ**: Language / Build Tool
- **ソース**: [Announcing TypeScript 7.0 RC](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-rc/), [Announcing TypeScript 7.0 Beta](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/)

## 概要

TypeScript 7.0 は、コンパイラ本体を TypeScript/JavaScript から **Go** へ移植（コードネーム「Corsa」/バイナリ名 `tsgo`）した最初のメジャーリリース。2026-06-18 に RC が npm 公開され、安定版（GA）は RC から約1ヶ月以内を目安に予定されている（コミット済みの確定日ではない）。

最大の売りはパフォーマンスで、Microsoft は大規模コードベースで **6.0 比 約10倍高速** の型チェックを実現したと報告している。数分かかっていた型チェックが数秒台に短縮されるケースもある。重要なのは「リライトではなくポート（移植）」である点で、型チェックのセマンティクスは 6.0 と同一に保たれている。RC は従来通り `tsc` バイナリを出荷する（nightly は引き続き `tsgo` 名）。

## 主な変更点

### ネイティブ + 並列化による高速化
- ネイティブコード速度と共有メモリ並列化の組み合わせで高速化。
- **チェッカー並列化**: デフォルトで型チェッカーワーカーが4つ稼働。`--checkers` で調整可能（メモリと引き換えにビルド時間短縮）。
- **プロジェクト参照ビルダー並列化**: `--builders` で複数プロジェクトの並列ビルドを制御。例 `--checkers 4 --builders 4` で最大16の型チェッカーが同時実行。
- **`--singleThreaded`**: デバッグやパフォーマンス比較用に単一スレッド動作を強制。

### テンプレートリテラル型の Unicode 改善
UTF-16 サロゲートペア分割から Unicode 単位の扱いへ改善。

```typescript
type HeadTail<S> = S extends `${infer Head}${infer Tail}`
  ? [Head, Tail] : never;

type Result = HeadTail<"😀abc">;
// 7.0: ["😀", "abc"]
// 6.0: ["\ud83d", "\ude00abc"]
```

### エディタ体験
- VS Code 向け「TypeScript Native Preview extension」が利用可能。
- LSP（Language Server Protocol）ベースで、複数スレッドによる並行リクエスト処理に対応。
- 言語サーバーコマンドの失敗が 6.0 比で 20倍以上削減。

## 破壊的変更・移行ガイド

### コンパイラオプションのデフォルト変更
7.0 では以下がデフォルト化される。

```json
{
  "strict": true,
  "module": "esnext",
  "target": "es2023",
  "noUncheckedSideEffectImports": true,
  "stableTypeOrdering": true,
  "types": []
}
```

特に `types: []`（従来は `@types/*` を暗黙的に全取り込み）と `rootDir` の挙動変更に注意。従来動作を戻すには明示指定が必要。

```json
{
  "compilerOptions": {
    "rootDir": "./src",
    "types": ["node", "jest"]
  }
}
```

### 廃止された機能
- `target: es5`、`downlevelIteration`
- `moduleResolution: node/node10`
- `module: amd, umd, systemjs`
- `baseUrl`
- `esModuleInterop: false`（無効化不可）

### JavaScript / JSDoc 対応の簡素化
- 値を型として使用不可（`typeof` を使用）。
- `@enum` の特殊処理を廃止。
- Closure 形式の関数構文・ポストフィックス `!` は非サポート。

### 6.0 との並行運用
移行期は 6.0 をエイリアスで併存させられる。

```bash
npm install -D typescript@rc          # 7.0 RC
npx tsc --version                      # Version 7.0.1-rc
```

```json
{
  "devDependencies": {
    "typescript": "npm:@typescript/typescript6@^6.0.0",
    "typescript-7": "npm:typescript@rc"
  }
}
```

## 今後の注目点

- 安定版 GA は RC から約1ヶ月以内が目安。移行前に CI で `types`/`rootDir`/`target` のデフォルト変更差分を検証しておくのが安全。
- プログラマティック API（コンパイラ API の公開）は 7.1 以降に持ち越し。ビルドツールや Lint 系ツールが tsgo に追随するかがエコシステム移行の鍵。
- Angular 22 が TypeScript 6 を必須にするなど、フレームワーク側の追随も進行中。
