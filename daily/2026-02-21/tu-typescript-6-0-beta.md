# TypeScript 6.0 Beta — JS ベースコンパイラ最終版の全貌

- **日付**: 2026-02-11（Beta リリース）/ 2026-03-17（安定版予定）
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/), [GitHub Releases](https://github.com/microsoft/typescript/releases)

## 概要

TypeScript 6.0 は、現行の JavaScript ベースコンパイラ（tsc）による**最後のメジャーリリース**となる。次期 TypeScript 7.0 は Go 言語で書き直されたコンパイラに移行し、5-10 倍のコンパイル速度、約 8 倍のエディタ起動改善、約 50% のメモリ削減を実現する予定。

6.0 では多くのデフォルト値の変更と非推奨オプションの追加により、7.0 への移行パスを整備している。既存プロジェクトは 6.0 の段階で互換性を確認し、非推奨オプションへの依存を解消しておくことが推奨される。

## 主な変更点

### 新機能

- **`this` を使用しない関数の文脈感度低下**: メソッド構文でも矢印関数と同様に型推論が動作するよう改善。`this` が実際に使用されない関数は文脈感度がないと判定される
- **サブパスインポート（`#/` 開始）**: Node.js の最新仕様に対応し、従来の `#root/*` から簡潔な `#/*` 形式が使用可能に
- **`--stableTypeOrdering` フラグ**: TS 7.0 への移行を支援する新フラグ。型の順序付けを安定化（最大 25% のパフォーマンスオーバーヘッドあり）
- **ES2025 サポート**: `RegExp.escape` など新しい組み込み API 型を追加
- **Temporal API 型**: Stage 3 の Temporal 提案に対応した組み込み型を提供
- **Map/WeakMap アップサートメソッド**: `getOrInsert` および `getOrInsertComputed` メソッドを追加
- **DOM ライブラリ統合**: `dom.iterable` と `dom.asynciterable` が `dom` に統合

### デフォルト値の変更

| オプション | 旧デフォルト | 新デフォルト |
|-----------|-------------|-------------|
| `strict` | `false` | `true` |
| `module` | 状況依存 | ESModule |
| `target` | `es3`/`es5` | `es2025` |
| `rootDir` | 推論 | `.`（tsconfig.json ディレクトリ） |
| `types` | 自動検出 | `[]`（明示的指定が必須） |

## 破壊的変更・移行ガイド

### TS 7.0 で削除予定の非推奨オプション

以下のオプションは 6.0 で非推奨となり、7.0 で完全に削除される：

- `target: es5` — モダンブラウザ対象へ
- `--downlevelIteration` — ES5 ターゲット廃止に伴い不要に
- `--moduleResolution node`（node10）— `node16`/`nodenext`/`bundler` に移行
- `--module amd/umd/systemjs` — ESModule に統一
- `--baseUrl`（パスマッピング用）— `paths` で相対パスを使用
- `--moduleResolution classic` — レガシー解決方式の廃止
- `esModuleInterop: false` — 常に true が前提に
- `--outFile` — バンドラー使用を前提に
- レガシー `module` 構文 — `namespace` に移行
- `asserts` キーワード — `with` に変更

### 互換性維持オプション

6.0 の段階では `tsconfig.json` に以下を追加することで非推奨オプションを引き続き使用可能：

```json
{
  "compilerOptions": {
    "ignoreDeprecations": "6.0"
  }
}
```

ただし、このオプションは TS 7.0 では機能しないため、早期の移行が推奨される。

### 移行ステップ

1. TypeScript 6.0 Beta をインストール: `npm install typescript@beta`
2. `--stableTypeOrdering` を有効化して型の順序変更による影響を確認
3. 非推奨警告を確認し、代替オプションに順次移行
4. `strict: true` がデフォルトになるため、明示的に `strict: false` を設定していないプロジェクトは挙動が変わる可能性がある

## 今後の注目点

- **TypeScript 7.0**: Go ベースコンパイラ。2026 年夏頃リリース予定。コンパイル速度 5-10 倍、メモリ使用量 50% 削減
- **エディタ対応**: 7.0 では VS Code、JetBrains IDE のエディタ起動が約 8 倍高速化
- **ES5 ターゲットの完全廃止**: 7.0 以降は ES2015+ のみサポート
- **Node.js ネイティブ TypeScript 実行**: Node.js の TypeScript ネイティブサポートとの連携強化
