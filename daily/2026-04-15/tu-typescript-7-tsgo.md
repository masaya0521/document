# TypeScript 7.0 (tsgo) — Go ベース新コンパイラの現状と移行ガイド

- **日付**: 2026-04-13（最新 dev preview: 7.0.0-dev.20260413.1）
- **カテゴリ**: Language
- **ソース**: [GitHub](https://github.com/microsoft/typescript-go), [npm @typescript/native-preview](https://www.npmjs.com/package/@typescript/native-preview), [Progress Update (2025/12)](https://devblogs.microsoft.com/typescript/progress-on-typescript-7-december-2025/)

## 概要

TypeScript 7.0 は「Project Corsa」として進められている Go ベースのネイティブコンパイラ書き換えプロジェクト。従来の JavaScript ベース `tsc` に対して 7-10x のビルド高速化を実現し、メモリ使用量も約50%削減される。2026年4月13日時点で dev preview ビルドが npm で公開されており、型チェック機能はほぼ完全（約20,000テストケース中、未対応は74件のみ）。

TypeScript 6.0（2026年3月23日リリース）が JavaScript ベース最後のメジャーバージョンとなり、7.0 への橋渡し役を担う。

## 主な変更点

### パフォーマンス

大規模プロジェクトでの実測値:

| プロジェクト | tsc | tsgo | 高速化倍率 |
|---|---|---|---|
| Sentry | 133秒 | 16秒 | 8.19x |
| VS Code | 89秒 | 8.7秒 | 10.2x |

- マルチスレッド対応により `--build` モードでの複数プロジェクト並列ビルドが可能
- インクリメンタルビルドはほぼ瞬時に完了
- エディタ起動時間は約8x 改善

### エディタサポート（VS Code 拡張）

`@typescript/native-preview` パッケージに同梱される VS Code 拡張で以下の機能が利用可能:

- 自動補完（自動インポート含む）
- 定義へ移動、型定義へ移動
- 名前変更、全参照検索
- ホバーツールチップ、シグネチャヘルプ
- リファクタリング

並列処理を活用したアーキテクチャ再設計により、安定性も向上。

### 型チェック互換性

- 約20,000個のコンパイラテストケースのうち、74個のみが未実装
- ほぼ完全な型チェック互換性を達成

## 破壊的変更・移行ガイド

### TypeScript 6.0 → 7.0 での変更

1. **API 非互換**: 既存の TypeScript Compiler API (`ts.createProgram` 等) はサポートされない。ツールチェーン（ESLint の `@typescript-eslint`、ts-morph 等）の対応が必要
2. **JavaScript チェック機能の変更**: JSDoc タグの一部（`@enum` 等）が削除
3. **emit ターゲット**: es2021 以降のみ対応
4. **6.0 のサポート終了方針**: セキュリティパッチと重大な回帰修正のみに限定

### 試す方法

```bash
# npm でインストール
npm install -D @typescript/native-preview

# tsgo コマンドで型チェック
npx tsgo --project tsconfig.json
```

VS Code 拡張は npm パッケージに同梱されており、インストール後に有効化できる。

### 移行チェックリスト

- [ ] `@typescript/native-preview` をインストールして既存プロジェクトで `tsgo` を実行
- [ ] 型エラーの差分を確認（ほぼ同一のはず）
- [ ] 使用しているツールチェーン（ESLint、Prettier 等）の tsgo 対応状況を確認
- [ ] CI で `tsc` と `tsgo` を並行実行して結果を比較

## 今後の注目点

- 2026年中盤（夏頃）に TypeScript 7.0 正式リリースが見込まれる
- エコシステムツール（`@typescript-eslint`、`ts-morph`、`type-coverage` 等）の 7.0 対応が鍵
- TypeScript 6.0 は長期サポートではなくブリッジリリースという位置づけ。早めの検証開始が推奨
- `--build` モードのマルチスレッド並列ビルドはモノレポ環境で特に大きな恩恵
