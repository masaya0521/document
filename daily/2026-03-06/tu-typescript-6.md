# TypeScript 6.0 — JavaScript ベース最後のメジャーリリース

- **日付**: 2026-03-06（RC: 2/24 リリース済、安定版: 3/17 予定）
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/), [GitHub Iteration Plan](https://github.com/microsoft/TypeScript/issues/63085), [Migration Guide](https://github.com/microsoft/TypeScript/issues/62508)

## 概要

TypeScript 6.0 は、現行の JavaScript ベースコンパイラとしては最後のメジャーリリースとなる。次期 TypeScript 7.0 では Go で書き直されたコンパイラ（tsgo）に移行し、5〜10倍のコンパイル高速化が見込まれている。6.0 はその橋渡しとして、モダンなデフォルト設定への変更やレガシーオプションの廃止を行い、エコシステムの移行準備を促すリリースである。

## 主な変更点

### 新機能
- **`#/` サブパスインポート**: `package.json` の `imports` フィールドを活用したモジュール解決
- **`es2025` ターゲット / lib**: 最新の ECMAScript 仕様をサポート
- **Temporal 型**: `Temporal` API の型定義を標準ライブラリに追加
- **`using` キーワード**: 自動リソース管理（Explicit Resource Management）のサポート
- **プライベートフィールドの `typeof` 推論改善**: より正確な型推論
- **ビルド速度**: 最大 30% のビルド高速化

### デフォルト設定の変更
- **strict モード**: 全コードが JavaScript strict モードとして扱われるように変更
- **モジュール解決**: `--module commonjs` で明示的な `moduleResolution` 指定がない場合、`node10` から `bundler` に変更
- 現代のエバーグリーンランタイムと ESM 主流の環境を反映したデフォルト値の調整

## 破壊的変更・移行ガイド

### 注意が必要な変更
1. **strict モードの強制**: `implements`, `interface`, `let`, `package`, `private`, `protected`, `public`, `static`, `yield` が予約語として扱われる。非モジュール・非 strict コードでこれらを変数名等に使用している場合はエラーになる
2. **`moduleResolution` のデフォルト変更**: CommonJS プロジェクトで暗黙的に `node10` を使っていた場合、挙動が変わる可能性がある
3. **Node.js 18+ が必須**: Node.js 16 以前はサポート外

### 移行手順
1. `tsc --noEmit` を実行してエラーを確認
2. ジェネリクスやテストの回帰をチェック
3. VS Code で「TypeScript: Restart TS Server」を実行
4. リンター（ESLint 等）や `tsconfig.json` の設定を更新

ほとんどのプロジェクトは TS 5.x との 95% 互換性があり、1 時間以内に移行可能とされている。

## 今後の注目点

- **TypeScript 7.0**（2026年中期予定）: Go ベースコンパイラ（tsgo）への完全移行。5〜10倍のコンパイル速度向上、ほぼ瞬時のインクリメンタルビルド、エディタ起動の約 8 倍高速化
- 6.0 で非推奨となったオプションは 7.0 で完全削除される見込み
- `--stableTypeOrdering` 診断フラグによる移行支援の活用
