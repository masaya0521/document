# TypeScript 6.0 — JavaScript 時代の終わりと Go リライトへの道

- **日付**: 2026-03-23
- **カテゴリ**: Language
- **ソース**: [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/03/23/typescript-6-0-ships-as-final-javascript-based-release-clears-path-for-go-native-7-0.aspx), [typescript.news](https://typescript.news/articles/2026-03-26-typescript-6-0-final-javascript-release)

## 概要

TypeScript 6.0 は **JavaScript で書かれた最後のバージョン**。strict モードのデフォルト化や ES5 ターゲットの廃止など、9 つのデフォルト設定を一斉に変更する大きな破壊的変更を含む。次期 TypeScript 7.0（Project Corsa）では Go でコンパイラが完全リライトされ、型チェック速度が約 10 倍に向上する見込み。

## 主な変更点

### デフォルト設定の変更（9 項目）

- **strict モード**: デフォルトで有効に
- **ES5 ターゲット**: コンパイルターゲットとして廃止
- **AMD / UMD モジュール**: 非推奨化
- その他、複数の tsconfig オプションのデフォルト値が変更

### なぜ Go でリライトするのか（Project Corsa）

Microsoft が Go を選択した理由:
- **目標はポート（移植）であり、リライト（再設計）ではない**: 12 年間進化してきた既存コードの構造を維持したい
- **共有可変状態**: TypeScript コンパイラは複雑な共有可変状態を多用しており、Rust の所有権モデルとは相性が悪い
- **Go のシンプルなパターン**: 既存コードの翻訳が容易
- **共有メモリマルチスレッド**: 並列型チェックに最適

### パフォーマンス改善の見込み

| ベンチマーク | 現行（TS 6） | tsgo（TS 7 プレビュー） |
|---|---|---|
| VS Code（150 万行）型チェック | 77 秒 | 7.5 秒 |

## 破壊的変更・移行ガイド

### TS 6.0 への移行

1. **tsconfig.json の確認**: 9 つのデフォルト変更により、明示的に設定していないオプションの挙動が変わる
2. **ES5 ターゲットの置き換え**: ES5 をターゲットにしていたプロジェクトは ES2015 以上に変更が必要
3. **AMD/UMD の移行**: ESM または CommonJS に移行を検討
4. **段階的アップグレード**: `strict: false` を明示的に設定することで旧動作を維持可能

### TS 7.0（Go リライト）への備え

- tsgo プレビューは利用可能だがまだ機能未完成
- 安定版リリースは 2026 年後半〜2027 年初頭の見込み
- API 互換性は完全ではないため、TypeScript Compiler API を直接使用しているツールは影響を受ける可能性あり

## 今後の注目点

- TypeScript 7.0（tsgo）のベータリリース時期
- Go リライトでの Language Service プロトコル互換性
- エディタ統合（VS Code、JetBrains）への影響
- サードパーティツール（ESLint の typescript-eslint、ts-morph 等）の対応状況
- コミュニティの Go リライトに対する実運用フィードバック
