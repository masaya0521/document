# TypeScript 6.0 — JavaScript ベースコンパイラ最終版と Go リライトへの道

- **日付**: 2026-03-23（正式リリース）
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [移行ガイド](https://gist.github.com/privatenumber/3d2e80da28f84ee30b77d53e1693378f)

## 概要

TypeScript 6.0 は、現行の JavaScript ベースコンパイラとしての **最終メジャーリリース** という特別な位置づけのバージョンである。次の TypeScript 7.0 では Go 言語で書き直されたネイティブコンパイラに移行し、VS Code の 150 万行のコードベースで型チェックが 77 秒から 7.5 秒へと劇的に高速化される。6.0 の変更の多くは、7.0 への移行を円滑にするための準備として設計されている。

## 主な変更点

### デフォルト値の刷新

TypeScript 6.0 では複数のコンパイラオプションのデフォルト値が変更された。

- **`strict`**: `true` がデフォルトに（以前は `false`）
- **`module`**: `esnext` に統一
- **`target`**: `es2025`（浮動ターゲット）に
- **`types`**: 空配列がデフォルト（明示的な指定が必須に）

### 新機能

**サブパスインポート（`#/` プレフィックス）**

Node.js の `#/` サブパスインポートに対応。従来の `#root/` より簡潔に記述可能。

```json
{
  "imports": {
    "#/*": "./dist/*"
  }
}
```

**メソッド推論の改善**

`this` を使用しないメソッド構文の関数で、型推論の順序依存問題が解消された。

**新しい標準ライブラリ**

- **Temporal API**（Stage 4 到達）の完全サポート
- `Map` / `WeakMap` の `getOrInsert` メソッド
- `RegExp.escape` 関数
- `es2025` target/lib の追加

## 破壊的変更・移行ガイド

### 廃止されるオプション

以下のオプションは 6.0 で非推奨となり、7.0 で完全に削除される。

| オプション | 移行先 |
|---|---|
| `target: "es5"` | `es2015` 以上を指定 |
| `--moduleResolution node` | `nodenext` または `bundler` に変更 |
| AMD / UMD / SystemJS モジュール | ESM に移行 |
| `--baseUrl` | `paths` に統合 |
| `--outFile` | 外部バンドラーを使用 |

### 一時的な回避策

廃止オプションは `"ignoreDeprecations": "6.0"` を `tsconfig.json` に追加することで一時的に無視できるが、7.0 では完全に削除されるため早期の移行が推奨される。

```json
{
  "compilerOptions": {
    "ignoreDeprecations": "6.0"
  }
}
```

### 推奨される移行手順

1. TypeScript 6.0 にアップデート
2. `tsc --noEmit` でエラーを確認
3. 廃止警告が出たオプションを順次移行
4. `strict: true` がデフォルトになったことによるエラーを解消
5. TypeScript 7.0 beta が出たら早期にテスト

## 今後の注目点

- **TypeScript 7.0**: Go ベースのネイティブコンパイラ。2026 年中のリリースが予定されている
- **パフォーマンス**: 7.0 では型チェック速度が約 10 倍に向上する見込み
- **互換性**: 7.0 は 6.0 と高い互換性を目指しているが、廃止オプションは完全に削除される
- **エコシステム**: VS Code の TypeScript 統合は既に 6.0 ベースに移行済み（VS Code February 2026 リリース）
