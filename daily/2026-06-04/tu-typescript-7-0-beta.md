# TypeScript 7.0 Beta — Go 製ネイティブコンパイラ（Project Corsa）

- **日付**: 2026-06-04（ベータ公開は 2026-04-21）
- **カテゴリ**: Language / Build Tool
- **ソース**: [TypeScript Blog — Announcing TypeScript 7.0 Beta](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/04/21/typescript-7-0-beta-arrives-on-go-based-foundation-with-10x-speed-claim.aspx)

## 概要

TypeScript 7.0 は、これまで TypeScript 自身（JavaScript）で書かれていたコンパイラ／言語サービスを **Go で全面的に書き直した**「Project Corsa」の成果である。2026-04-21 に公開ベータが登場し、現在は安定版に向けた最終段階にある。RC は 6 月後半〜7 月初旬、安定版はその後数週間以内が見込まれている。

最大の特徴は性能で、`tsc` 比で **およそ 10 倍高速**。Microsoft の計測では、150 万行の VS Code コードベースのコンパイルが従来の 78 秒から **7.5 秒** に短縮された。ネイティブコード化に加え、共有メモリによる並列処理が高速化を支える。

## 主な変更点

- **ネイティブ実装**: Go 製の新コンパイラは `tsc` ではなく `tsgo` から起動する。
- **並列化フラグ**:
  - `--checkers`: 型チェッカーのワーカー数（デフォルト 4）
  - `--builders`: プロジェクト参照ビルドの並列数
  - `--singleThreaded`: シングルスレッド実行の強制
- **配布形態**: `@typescript/native-preview@beta` として npm 配布。VS Code 向けに「TypeScript Native Preview」拡張も提供。

```bash
npm install -D @typescript/native-preview@beta
npx tsgo --version   # Version 7.0.0-beta
```

## 破壊的変更・移行ガイド

7.0 では古い設定・出力ターゲットが整理される。主なものは以下。

- `target: es5` / `downlevelIteration` のサポート終了
- `baseUrl` の削除、`moduleResolution: node` / `classic` の廃止
- `types` のデフォルトが `[]` に変更（必要な型は明示指定が必須）
- `rootDir` のデフォルトが `./` に変更され、設定調整が必要な場合あり
- `stableTypeOrdering` は常に有効（無効化不可）

移行期の互換策として、`@typescript/typescript6` パッケージが `tsc6` バイナリを提供し、6.0 と 7.0 を並行利用できる。まずは `tsgo` で既存プロジェクトをビルド／型チェックして差分を検証するのが安全。

## 今後の注目点

- RC は数週間以内、安定版はそこから 2 か月以内のスケジュール感。
- 安定したプログラマティック API は **7.1 以降** で提供予定（ESLint や各種ツールの本格対応はこの段階が目安）。
- Go 化による並列処理の効果は大規模モノレポほど大きく、CI 時間短縮のインパクトが期待される。
