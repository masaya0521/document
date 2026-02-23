# TypeScript 6.0 Beta — JavaScript ベース最後のリリース

- **日付**: 2026-02-11
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/), [InfoQ](https://www.infoq.com/news/2026/02/typescript-6-released-beta/)

## 概要

TypeScript 6.0 Beta は 2026 年 2 月 11 日に発表された、JavaScript ベースのコンパイラとしては最後のメジャーリリースとなるバージョン。次期 TypeScript 7.0 では Go 言語で書き直されたネイティブコンパイラへ移行予定であり、6.0 はその移行を円滑に進めるための「橋渡しリリース」として位置づけられている。strict モードのデフォルト化、レガシーオプションの廃止、最新 ECMAScript 仕様への対応が主な変更点。

## 主な変更点

### デフォルト値の変更

| オプション | 旧デフォルト | 新デフォルト |
|-----------|------------|------------|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | `es3` | `es2025` |
| `rootDir` | 入力ファイルから推定 | `.`（tsconfig.json のディレクトリ） |
| `types` | 全 `@types` パッケージ | `[]`（空配列） |

### 新機能

- **サブパスインポート（`#/` 記法）**: Node.js の `#/` で始まるサブパスインポートを TypeScript がネイティブサポート
- **Temporal API 型定義**: Stage 3 の Temporal API のビルトイン型を追加
- **`RegExp.escape`（ES2025）**: 正規表現エスケープのサポート
- **Map/WeakMap の新メソッド**: `getOrInsert` と `getOrInsertComputed` メソッドの型サポート
- **`es2025` ターゲット**: 新しいコンパイルターゲットオプション
- **`--moduleResolution bundler` と `--module commonjs` の組み合わせ**: 従来互換性がなかった設定の組み合わせが可能に
- **DOM lib 統合**: `lib.dom.iterable` と `lib.dom.asynciterable` が `lib.dom` に統合され、設定が簡略化

### コンテキスト感度の改善

`this` を使用しない関数が型推論時により優先されるようになり、メソッド構文の関数でもアロー関数と同様の型推論が機能する。

## 破壊的変更・移行ガイド

### 廃止されたオプション

以下のオプションは 6.0 で非推奨、7.0 で完全削除予定：

- **`--target es5`**: 最低ターゲットは `ES2015` に変更
- **`--module amd/umd/systemjs`**: レガシーモジュールシステムの廃止
- **`--moduleResolution classic`**: クラシック解決の廃止
- **`--outFile`**: ファイル結合出力の廃止
- **`--baseUrl`**: 非推奨化
- **`--downlevelIteration`**: ES5 ターゲット廃止に伴い不要に
- **`module` キーワード**: `namespace` キーワードに完全移行
- **import assertions**: `asserts` 構文から `with` 構文への移行

### 移行手順

1. **tsconfig.json の確認**: `strict: true` が既に設定されていれば影響は最小限
2. **ターゲットの確認**: `target: "es5"` を使用している場合は `es2015` 以上に変更
3. **モジュールシステムの確認**: AMD/UMD/SystemJS を使用している場合はバンドラーへの移行を検討
4. **`--baseUrl`**: パスマッピングに `paths` オプションを使用するよう変更
5. **`module` キーワード**: `namespace` キーワードに置換

```jsonc
// tsconfig.json の推奨設定（TS 6.0 以降）
{
  "compilerOptions": {
    "target": "es2025",
    "module": "esnext",
    "moduleResolution": "bundler",
    "strict": true
  }
}
```

## 今後の注目点

- **TypeScript 7.0**: Go 言語による完全書き直し版。8〜10 倍のビルド速度改善が実証済み（VS Code 150 万行のコンパイルが 89 秒 → 8.74 秒）
- 6.0 の正式リリース時期（Beta からの GA は数週間以内の見込み）
- 7.0 への移行パスと、既存エコシステム（ESLint, Prettier 等）の対応状況
- Deno 2.6 が既に tsgo（Go 版 TypeScript 型チェッカー）を実験的に統合しており、エコシステム全体での採用が加速する可能性
