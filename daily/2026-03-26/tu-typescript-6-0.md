# TypeScript 6.0 — JS ベース最後のリリースと 7.0 移行準備

- **日付**: 2026-03-23
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/03/23/typescript-6-0-ships-as-final-javascript-based-release-clears-path-for-go-native-7-0.aspx)

## 概要

TypeScript 6.0 は、JavaScript で書かれた従来のコンパイラをベースとする**最後のメジャーリリース**である。次期 TypeScript 7.0 は Go 言語で書き直されたネイティブコンパイラ（tsgo）をベースとし、マルチスレッド対応により 8〜10 倍の高速化を実現する。6.0 はこの移行を円滑に進めるための「橋渡し」リリースとして位置づけられ、多数のデフォルト値変更と非推奨化を含む。

## 主な変更点

### デフォルト値の変更

6.0 で最も影響が大きいのはデフォルト値の変更である。

| オプション | 旧デフォルト | 新デフォルト |
|----------|-----------|-----------|
| `strict` | `false` | **`true`** |
| `module` | 変動 | **`esnext`** |
| `target` | 変動 | **`es2025`** |
| `types` | すべて自動検出 | **空配列 `[]`** |
| `rootDir` | 推論 | **`tsconfig.json` のディレクトリ** |

特に `types` が空配列になる変更は影響が大きく、`@types/node` 等を使用するプロジェクトは `"types": ["node"]` の明示的指定が必要になる。

### 新機能

- **型推論の改善**: ジェネリック呼び出しにおけるアロー関数とメソッド構文の扱いが統一
- **サブパスインポート**: Node.js 20 以降で `#/` で始まるサブパスインポートに対応
- **`--moduleResolution bundler` + `--module commonjs`**: この組み合わせが許可
- **`es2025` ターゲット**: `RegExp.escape` 等を含む
- **Temporal API 型**: ステージ 4 達成に伴う組み込み型サポート
- **Map/WeakMap upsert**: `getOrInsert`、`getOrInsertComputed` メソッド
- **DOM 型統合**: `dom.iterable` と `dom.asynciterable` が `dom` に統合
- **`--stableTypeOrdering`**: 6.0 と 7.0 の型順序を統一するフラグ（性能トレードオフあり）

### 削除・非推奨化されたオプション

以下のオプションが削除または非推奨化された。これらは 7.0 では完全に削除される。

**削除:**
- `target: es5`
- `--downlevelIteration`
- `--moduleResolution node`（node10）/ `classic`
- `--module amd` / `umd` / `systemjs`
- `--outFile`
- `--baseUrl`

**強制有効化:**
- `esModuleInterop` と `allowSyntheticDefaultImports` が常に有効
- `alwaysStrict: false` は不可（すべてストリクトモード）

**廃止構文:**
- レガシー `module` キーワード（`namespace` を推奨）
- import assertions（`assert` → `with` に移行）
- `/// <reference no-default-lib/>` ディレクティブ

### コマンドライン動作の変更

`tsconfig.json` が存在するディレクトリで `tsc file.ts` のようにファイルを直接指定するとエラーになる。回避するには `--ignoreConfig` フラグを使用する。

## 破壊的変更・移行ガイド

### 影響度の高い変更への対応

1. **`types` デフォルト変更**: `tsconfig.json` に `"types": ["node"]` 等を明示的に追加する
2. **`strict: true` デフォルト化**: 既に `strict: true` を設定しているプロジェクトは影響なし。そうでない場合は個別の strict フラグ（`noImplicitAny` 等）を段階的に有効化
3. **`target: es5` 削除**: ES5 をターゲットにしているプロジェクトは `es2015` 以上に移行が必要
4. **`--moduleResolution node` 削除**: `node16` または `bundler` に移行

### 推奨移行手順

```bash
# 1. TypeScript 6.0 にアップグレード
npm install typescript@6.0

# 2. 非推奨警告を確認
npx tsc --noEmit

# 3. tsconfig.json を更新（types の明示的指定等）

# 4. TypeScript 7.0 ネイティブプレビューで事前検証
npm install @typescript/native-preview
npx tsgo --noEmit
```

## 今後の注目点

- **TypeScript 7.0**: Go ネイティブコンパイラ（tsgo）ベース。2026 年 1 月に安定版リリース済み。6.0 で非推奨警告が出た項目は 7.0 で完全削除される
- **エコシステム対応**: 主要なエディタ（VS Code, IntelliJ）や lint ツール（ESLint）の 6.0 / 7.0 対応状況
- **`--stableTypeOrdering`**: 6.0 → 7.0 移行時に型の順序差異によるテスト失敗を防ぐために有用
