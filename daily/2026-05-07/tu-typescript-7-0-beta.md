# TypeScript 7.0 Beta — Project Corsa による Go 製コンパイラ

- **日付**: 2026-05-07
- **カテゴリ**: Language / Build Tool
- **ソース**: [TypeScript Blog (2026-04-21)](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/04/21/typescript-7-0-beta-arrives-on-go-based-foundation-with-10x-speed-claim.aspx), [InfoWorld](https://www.infoworld.com/article/4100582/microsoft-steers-native-port-of-typescript-to-early-2026-release.html)

## 概要

Microsoft は TypeScript 7.0 Beta を 2026-04-21 に公開した。これは「Project Corsa」と呼ばれる、TypeScript コンパイラ自体を Go 言語で書き直すプロジェクトの成果物。従来の TypeScript コンパイラ（tsc）は TypeScript 自身で書かれて JavaScript にコンパイルされていたが、7.0 では Go ネイティブコードとして配布される。

公称値で **TypeScript 6.0 比 約 10 倍高速**。型チェックロジックは 6.0 と構造的に同一に保たれており、既存プロジェクトはほぼ無修正で動作する想定。安定版（7.0 GA）は 2026 年 6 月頃を目標とし、その数週間前に RC が出る予定。

## 主な変更点

### ネイティブコンパイラへの移行

- 既存の TypeScript コードベースから機械的に Go へ移植
- LLVM ではなく Go の標準ツールチェーンでコンパイル
- shared memory parallelism を活用し、マルチコア環境での型チェックが大幅に高速化

### パフォーマンス（公称値）

- 大規模リポジトリ（Bloomberg / Canva / Figma / Google / Lattice / Linear などで先行検証済）で「ビルド時間が大半削れた」との報告
- 単純なベンチで約 10×、IDE 内のインクリメンタル型チェックでも体感差が大きい

### 互換性

- 型チェックの**意味論は 6.0 と同一**（バグ互換まで意識して移植）
- 既存の `tsc` API、`tsserver` プロトコル、tsconfig.json は維持
- 一部内部 API に依存していたツール（ESLint プラグイン、ts-node 等）は対応リリースが必要

### 配布形態

- 単一バイナリ（Go 製）として配布
- Node.js を経由しない実行が可能
- npm パッケージ経由でのインストールも引き続きサポート（バイナリラッパー）

## 破壊的変更・移行ガイド

互換性を最優先に設計されているため、**ほとんどのユーザはコード変更不要**。ただし以下に注意。

- **コンパイラ内部 API に依存するツール**: 一部の AST 走査・カスタム transformer は再ビルドが必要
- **`tsc --build` の挙動差**: 並列化により、依存順序の前提に依存していたビルドスクリプトで挙動が変わる可能性
- **エラーメッセージの微差**: 内容は同等だが、フォーマットや行番号計算ロジックの一部が更新

移行手順（推奨）:
1. CI でまず TypeScript 7.0 Beta を並走させ、既存ビルドの差分を確認
2. ESLint / ts-jest / ts-node など内部 API を使うツールの 7.0 対応版に揃える
3. tsconfig の `compilerOptions` をそのまま流用可能だが、新規追加された並列化系オプションがあれば検討

## 今後の注目点

- **GA リリース時期**: 6 月頃の見込み。RC が出るタイミングで本番採用の判断を
- **Bun / Deno など他ランタイムでの取り込み**: Go 製バイナリ前提だが、tsc API 互換性は維持
- **エコシステム対応**: ESLint typescript-eslint、ts-jest、ts-node、tsx などの主要ツールがいつ 7.0 対応するか
- **Project Corsa 以後**: Go ベースになることで言語仕様の進化速度がどう変わるか（実装制約の緩和に伴う新機能追加の余地）
