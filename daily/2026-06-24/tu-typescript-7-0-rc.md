# TypeScript — 7.0 RC（Go ネイティブコンパイラ / Project Corsa）

- **日付**: 2026-06-24（RC リリースは 2026-06-18）
- **カテゴリ**: Language
- **ソース**: [microsoft/typescript-go](https://github.com/microsoft/typescript-go), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/03/23/typescript-6-0-ships-as-final-javascript-based-release-clears-path-for-go-native-7-0.aspx), [TypeScript 6.0 解説（socket.dev）](https://socket.dev/blog/typescript-6-0-will-be-the-last-javascript-based-major-release)

## 概要

2026-06-18、TypeScript 7.0 が Release Candidate（RC）に到達した。最大の変更は、14 年間 TypeScript 自身（JavaScript）で書かれてきたコンパイラを **Go に移植した** こと。コードネームは Project Corsa、ネイティブバイナリは `tsgo` と呼ばれる。Microsoft は型チェックが **約 10 倍高速**、メモリ使用量は **約半減** と報告しており、GA（正式版）は RC から約 1 ヶ月後を見込んでいる。

直前の TypeScript 6.0（2026-03-23）が「JavaScript ベースの最後のメジャー」として strict デフォルト化・ESM デフォルト化などの破壊的変更を済ませており、7.0 はその設定変更を引き継いだ上で実装基盤を Go へ切り替える位置づけになっている。

## 主な変更点

### パフォーマンス（実測値）

| プロジェクト | 行数 | 向上倍率 | 詳細 |
|-------------|------|---------|------|
| VS Code | 1.5M 行 | 10.4 倍 | 77.8 秒 → 7.5 秒 |
| Playwright | 356K 行 | 10.1 倍 | 11.1 秒 → 1.1 秒 |
| TypeORM | 270K 行 | 13.5 倍 | 17.5 秒 → 1.3 秒 |
| Sentry | — | 8.19 倍 | 133 秒 → 16 秒 |

- エディタのプロジェクト読み込み: 約 8 倍高速化（9.6 秒 → 1.2 秒）
- 高速化の内訳: ネイティブバイナリ実行で 3〜4 倍、ワーカースレッド間の共有メモリ並列化（goroutine）で 2〜3 倍

### 移植の方針

- 既存の TS/JS コンパイラを「行単位で Go に移植」した形で、アルゴリズムとデータ構造は維持。型検査の意味論は同一に保たれている。
- 新しい並列化向けフラグが追加: `--checkers N`（型チェッカーのワーカー数、既定 4）、`--builders N`（プロジェクト参照の並列ビルド数、既定 16）、`--singleThreaded`（並列処理を無効化）。

### なぜ Go なのか

Rust の所有権モデルは循環参照を禁止するが、TypeScript コンパイラの AST とシンボルテーブルは循環参照を多用する。Go の GC モデルと goroutine による並列化がこの構造に適合したため採用された。

## 破壊的変更・移行ガイド

7.0 は 6.0 で導入された厳密デフォルトを引き継ぐ。主な非互換は次のとおり。

### tsconfig.json のデフォルト変更

- `rootDir` の既定が `./` に（明示指定が事実上必須）
- `types` の既定が空配列に（`@types/*` は明示指定が必要）

### 削除された設定オプション

- `target: es5`（最小が es2015 に）
- `moduleResolution: node`（`nodenext` または `bundler` を使用）
- `baseUrl`（相対パスで `paths` を指定）
- `esModuleInterop: false`、`amd` / `umd` / `systemjs` / `none` モジュール形式

### その他

- テンプレートリテラル型の推論で、絵文字・マルチバイト文字を単一の Unicode コードポイントとして扱う
- JSDoc サポートの簡略化（`@enum` タグ削除など）

### 移行手順

```bash
# RC 版（推奨）
npm install -D typescript@rc

# 6.0 と並行運用するためのエイリアス
npm install -D typescript@npm:@typescript/typescript6
```

推奨ロールアウト:

1. **今すぐ**: `tsc` CLI と CI の型チェックを 7.0 へ
2. **待機**: typescript-eslint / ts-morph / カスタムトランスフォーマーは安定 API（7.1 予定）まで保留
3. **段階的**: エディタ拡張は開発者ごとにオプトイン
4. **本番切替**: GA と自社テストスイートの成功を確認してから

事前検証として、6.0 で `--stableTypeOrdering` を有効化して型の並び順差分を確認しておくと安全。

## 今後の注目点

- **プログラマティック API は 7.1 まで延期**: 安定したコンパイラ API（型情報を読むツール群が依存）は数ヶ月先。エコシステム対応は段階的になる。
- **GA 時期**: RC から約 1 ヶ月、すなわち 2026 年 7 月中の正式リリースが目安。
- **`tsgo` の呼称**: RC の標準パッケージでは `tsc` バイナリ自体が Go ネイティブ。nightly では引き続き `tsgo` 名で配布される。
