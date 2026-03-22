# TypeScript 6.0 RC — Go ベース TypeScript 7.0 への橋渡し

- **日付**: 2026-03-06
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/03/06/typescript-6-0-rc-bridges-to-go-based-future.aspx)

## 概要

TypeScript 6.0 RC は、現行の JavaScript ベースコンパイラとしての **最後のメジャーリリース** となる予定。次期 TypeScript 7.0 は Go で書き直されたコンパイラ・言語サービスを基盤とし、ネイティブコードと共有メモリマルチスレッドの利点を活かした大幅な高速化が見込まれる。6.0 はその移行を円滑にするための「ブリッジリリース」として位置づけられている。

## 主な変更点

### 新機能
- **`this` を使用しない関数の推論改善**: ジェネリック関数でのメソッド構文における型推論が改善
- **サブパスインポート（`#/` 構文）**: Node.js の新しいインポート仕様に対応し、簡潔なパスマッピングが可能に
- **`--stableTypeOrdering` フラグ**: TypeScript 7.0 への移行を支援する新フラグ。型の順序付けを安定化させ、Go ベースコンパイラとの一貫性を確保
- **ES2025 対応**: `RegExp.escape`、Temporal API、`Map`/`WeakMap` の `upsert` メソッドに対応

### デフォルト値の変更
- `strict: true` がデフォルトに
- `module` が `ESNext` をデフォルトに
- `target` が `ES2025` をデフォルトに
- `types: []` がデフォルトに（明示的な型定義パッケージ指定が必要）

## 破壊的変更・移行ガイド

TypeScript 6.0 は多数の破壊的変更を含む。移行時は以下に注意:

1. **ES5 / AMD / UMD / SystemJS の完全削除**: これらの出力ターゲット・モジュール形式はサポート終了。レガシーブラウザ対応が必要な場合はバンドラー側で対応
2. **`baseUrl` の廃止**: パスマッピングには `paths` や新しいサブパスインポートを使用
3. **`moduleResolution: classic` の廃止**: `node16` / `nodenext` / `bundler` に移行
4. **`rootDir` の推論廃止**: 明示的な指定が必要
5. **`strict: true` のデフォルト化**: 既存プロジェクトで strict モードを使用していなかった場合、型エラーが発生する可能性

### 移行手順
```jsonc
// tsconfig.json の推奨設定（6.0 向け）
{
  "compilerOptions": {
    "target": "ES2025",        // 明示推奨
    "module": "ESNext",        // 明示推奨
    "moduleResolution": "bundler", // classic からの移行先
    "strict": true,            // デフォルト化されたが明示推奨
    "stableTypeOrdering": true // 7.0 移行準備
  }
}
```

## 今後の注目点

- **TypeScript 7.0（Go ベースコンパイラ）** のリリース時期（2026 年後半の見込み）
- Go ベースコンパイラでの型チェック速度の実測値
- エディタ・言語サービスの応答性改善
- サードパーティツール（ESLint、Prettier 等）の TypeScript 7.0 対応状況
