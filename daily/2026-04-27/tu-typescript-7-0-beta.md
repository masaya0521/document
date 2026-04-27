# TypeScript 7.0 Beta — Go 製コンパイラと 10倍高速化の中身

- **日付**: 2026-04-27
- **カテゴリ**: Language
- **ソース**: [Microsoft 公式アナウンス](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/04/21/typescript-7-0-beta-arrives-on-go-based-foundation-with-10x-speed-claim.aspx), [microsoft/typescript-go](https://github.com/microsoft/typescript-go)

## 概要

Microsoft は 2026-04-21 に **TypeScript 7.0 Beta** を公開した。これは数年来開発されてきた "Project Corsa"（コードネーム） の集大成で、コンパイラと言語サービスを **TypeScript（JavaScript）から Go へ全面移植** した最初の公開ベータである。型チェック挙動とセマンティクスは 6.0 と同等を保ったまま、ネイティブコード実行と共有メモリ並列化により **多くのケースで 6.0 比 10倍高速** という。VS Code リポジトリ（約 150 万行）の単発ビルドでは tsc 78 秒に対し tsgo 7.5 秒という実測値が示されている。

ベータは `@typescript/native-preview@beta` という別パッケージ名で配布され、エントリポイントは `tsgo`。これにより既存の `tsc` と並走でき、CI や開発環境での比較・検証が容易になっている。

## 主な変更点

### Go 移植によるアーキテクチャ刷新

- 全コンパイラパスを Go に書き直し、ネイティブバイナリで起動する。
- 型チェッカーが**並列実行**可能になり、`--checkers <N>`（デフォルト 4）でワーカー数、`--builders` でプロジェクト参照ビルド並列度、`--singleThreaded` でシングルスレッドモードを制御できる。
- VS Code の言語サービスでも**「数か月にわたるドッグフーディングで安定」**しているとされ、TypeScript Native Preview 拡張から利用可能。

### インストールと使い方

```bash
npm install -D @typescript/native-preview@beta
npx tsgo --version
```

最終リリースでは従来通り `typescript` パッケージ／`tsc` コマンドに収束する予定。

### デフォルト設定の刷新

- `strict: true` がデフォルトに昇格。
- `module: "esnext"`、`rootDir: "./"`、`types: []`（従来の暗黙の全型読み込みを停止）。
- `noUncheckedSideEffectImports: true`、`stableTypeOrdering: true`（無効化不可）。

## 破壊的変更・移行ガイド

### 廃止された設定・機能

- `target: "es5"` を**サポート外**。`downlevelIteration` も廃止。
- `--outFile` による単一ファイル出力を削除。
- `baseUrl` 廃止（`paths` 内で相対パスを書く）。
- `esModuleInterop` / `allowSyntheticDefaultImports` を `false` に固定不可（実質常に有効化）。
- モジュール解決は `node` / `node10` から **`nodenext` または `bundler` へ** 移行が推奨。

### JavaScript／JSDoc 分析の整理

JS 解析の特殊ケースを大幅に削減し、TS との分析を統一。`@enum` や `@class` 等の JSDoc 特殊構文は非推奨化。

### 6.0 → 7.0 の互換性

公式は次のように述べている: 「TypeScript 6.0 で `stableTypeOrdering` を有効化した状態でクリーンにコンパイルされるコードは、7.0 でも同じ結果でコンパイルされるはず」。実務上は **6.x で `stableTypeOrdering` を先に有効化** し差分を解消してから 7.0 に上げる、という二段階移行が現実解になる。

## 今後の注目点

- **安定版は 2026-06 末予定**、その数週間前に RC が出る見込み。
- `@typescript/native-preview` は配布専用名であり、最終的に `typescript` 本体に統合される。CI で先行採用する場合はパッケージ名の切り替えを設計しておきたい。
- 並列化フラグ（`--checkers` / `--builders`）の実効値はマシン構成と TS プロジェクト形状で大きく変わるため、`tsc --diagnostics` と `tsgo --diagnostics` の両方で計測比較するのが推奨。
- API 利用（`typescript` の Programmatic API、ts-node、ts-loader、ESLint パーサなど）は **互換性レイヤの整備状況に依存**する。エコシステム側の対応スピードが採用判断のクリティカルパスになる。
