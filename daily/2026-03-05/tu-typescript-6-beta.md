# TypeScript 6.0 Beta — Go ベース TypeScript 7.0 への架け橋

- **日付**: 2026-03-05
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/), [InfoQ](https://www.infoq.com/news/2026/02/typescript-6-released-beta/), [Migration Guide](https://github.com/microsoft/TypeScript/issues/62508)

## 概要

TypeScript 6.0 は、Go で書き直された TypeScript 7.0（Project Corsa）への移行を見据えた「架け橋」リリースである。新機能の追加よりも、レガシーオプションの非推奨化とデフォルト設定のモダナイズに重点を置いている。6.0 で非推奨となった機能は 7.0 で完全に削除されるため、今のうちに移行を進めることが推奨される。

## 主な変更点

### 新機能

- **`using` 宣言**: `Symbol.dispose` によるリソースの自動破棄をサポート。DB コネクションやファイルストリームの管理が安全に

```typescript
{
  using file = openFile("data.txt");
  // スコープ終了時に自動的に file[Symbol.dispose]() が呼ばれる
}
```

- **Private フィールドの `typeof` 推論精度向上**: プライベートフィールドに対する型推論がより正確に
- **Subpath imports**: Node.js モジュール仕様の subpath imports をサポート
- **RegExp Escaping**: ECMAScript Stage 4 提案の RegExp Escaping をサポート
- **ビルド速度**: 最大 30% のビルド高速化

### デフォルト設定の変更

| 設定項目 | 旧デフォルト | 新デフォルト |
|----------|------------|------------|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | `es3` | `es2025` |
| `rootDir` | ソースファイルの共通祖先 | `tsconfig.json` のディレクトリ |
| `types` | 全 `@types/*` を自動インクルード | 空配列（明示的指定が必要） |

### 非推奨化された設定

以下は `"ignoreDeprecations": "6.0"` で一時的に抑制可能だが、7.0 で完全削除される：

- `moduleResolution: "classic"` → `nodenext` または `bundler` へ移行
- `esModuleInterop: false` / `allowSyntheticDefaultImports: false` → 常に有効化
- `target: "es5"` → 最低 `es2015` に変更
- `outFile` + namespaces パターン

## 破壊的変更・移行ガイド

### モダンプロジェクトの場合

ES Modules を使用し、`strict: true` を既に設定しているプロジェクトはほぼ影響なし。`npm install typescript@beta` でアップグレードし、ビルドが通ることを確認すれば十分。

### レガシープロジェクトの場合

1. **`target` の更新**: `es5` を使用している場合は `es2015` 以上に変更
2. **`moduleResolution` の更新**: `classic` → `nodenext` または `bundler`
3. **`esModuleInterop` の確認**: 明示的に `false` にしている場合は削除
4. **`types` フィールドの確認**: 自動インクルードに依存している場合は明示的に指定
5. **段階的移行**: `"ignoreDeprecations": "6.0"` を設定し、警告を順次解消

```jsonc
// tsconfig.json - 移行中の設定例
{
  "compilerOptions": {
    "ignoreDeprecations": "6.0",
    // 他の設定はそのまま。非推奨警告を順次解消していく
  }
}
```

## 今後の注目点

- **TypeScript 7.0（Project Corsa）**: Go で書き直されたコンパイラ。7〜10 倍のビルド高速化が報告されている。`@typescript/native-preview` パッケージで先行体験可能
- **tsgo コマンド**: TypeScript 7.0 のネイティブコンパイラのプレビュー版。`npm install -D @typescript/native-preview` でインストール可能
- **6.0 → 7.0 の移行**: 6.0 で非推奨警告を解消しておけば、7.0 へのアップグレードはスムーズになる見込み
- **リリース時期**: TypeScript 7.0 は 2026 年中盤のリリースが予定されている
