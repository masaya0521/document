# TypeScript — 7.0 RC（Go ネイティブコンパイラ / Project Corsa）

- **日付**: 2026-06-22
- **カテゴリ**: Language / Build Tool
- **ソース**: [公式 Beta 告知](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/04/21/typescript-7-0-beta-arrives-on-go-based-foundation-with-10x-speed-claim.aspx), [TypeScript 7.0 RC ガイド](https://www.digitalapplied.com/blog/typescript-7-0-rc-go-native-compiler-2026-upgrade-guide)

## 概要

TypeScript 7.0 の RC（Release Candidate）が 2026年6月18日 に公開された。最大の変更点は、これまで TypeScript/JavaScript で書かれていたコンパイラを **Go でネイティブ再実装した**点（コードネーム「Project Corsa」、配布物は `tsgo`）。アルゴリズム・データ構造・型チェックのセマンティクスは従来と同一に保ちつつ、ネイティブコンパイル化と並列処理によって **型チェックが従来比 約10倍高速** になった。マイクロソフトは安定版 GA を RC から約1ヶ月以内に予定しており、今が CI や評価用途で本格的に試せるタイミングとなる。

代表的なベンチマークとして、VS Code のコードベース（約150万行の TypeScript）の型チェックが **77秒 → 7.5秒** に短縮された。

## 主な変更点

- **Go ネイティブ実装**: コンパイラを JavaScript から Go へファイル単位で移植。同一アルゴリズム・同一データ構造を維持し、型チェック結果の互換性を確保
- **並列処理対応**: 解析（parse）・型チェック・エミットを複数スレッドで実行
  - `--checkers`: 型チェッカーワーカー数（デフォルト 4）
  - `--builders`: プロジェクト参照のビルダー数
  - `--singleThreaded`: シングルスレッド強制モード
- **デフォルト設定の厳格化**:
  - `strict: true`
  - `module: esnext`
  - `types: []`（グローバル型は明示列挙が必須に）
- **JavaScript サポートの整理**: JSDoc 構文の簡潔化、Closure スタイルの廃止
- **非推奨機能の削除**: `target: es5`、`downlevelIteration`、旧モジュール解決オプション
- **エディタ体験**: VS Code 向けに Native Preview 拡張を提供

## 破壊的変更・移行ガイド

- **並行運用が可能**: 安定版到達前は `@typescript/native-preview` パッケージ経由で `tsgo` コマンドを利用でき、既存の `tsc`（6.0）と並行運用できる
- **`rootDir` の明示**: 外部 `tsconfig.json` を参照する構成では `rootDir` の明示指定が必要になるケースがある
- **グローバル型の明示**: `types: []` がデフォルトになったため、`@types/node` などグローバル型定義は `types` 配列に明示列挙する
- **削除されたターゲット/オプションの置換**: `target: es5` や `downlevelIteration` に依存している場合は設定の見直しが必要

## 今後の注目点

- **安定版 GA**: RC から約1ヶ月以内（2026年6月下旬〜7月上旬目処）
- **プログラマティック API**: 安定版の API は TypeScript 7.1 以降で提供予定
- **未実装機能**: 効率的な `--watch` モード、JavaScript からの宣言ファイル生成（`.d.ts`）のパリティは今後対応
- ts-morph や ESLint type-aware ルールなど、TypeScript の内部 API に依存するツールチェーンの 7.0 対応状況を注視する必要がある
