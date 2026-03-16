# TypeScript 6.0 GA — JS ベース最後のメジャーリリース

- **日付**: 2026-03-17
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog (RC 発表)](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [InfoWorld](https://www.infoworld.com/article/4143186/typescript-6-0-reaches-release-candidate-stage.html)

## 概要

TypeScript 6.0 は、現行の JavaScript ベースコンパイラによる**最後のメジャーリリース**である。次期 TypeScript 7.0 では Go で再実装されたコンパイラ・言語サービスに移行し、ネイティブコードと共有メモリマルチスレッディングによる大幅なパフォーマンス向上が予定されている。

6.0 では `strict: true` のデフォルト化や非推奨オプションの整理など、7.0 への移行を見据えた「地固め」的な変更が多く含まれる。同時に ES2025 の新機能（Temporal API, RegExp.escape）への型サポートも追加された。

## 主な変更点

### デフォルト値の変更

TypeScript 6.0 では複数のコンパイラオプションのデフォルトが変更された:

- **`strict: true`** がデフォルトに（これまでは `false`）
- **`module: esnext`** がデフォルトに（モダンな ESM ベース）
- **`target: es2025`** がデフォルトに（最新の JavaScript に対応）
- **`types: []`** がデフォルトに（`@types/*` の自動読み込みを廃止）

### ES2025 対応

- **Temporal API**: Stage 3 に到達した Temporal 提案の組み込み型を追加。`Temporal.PlainDate`, `Temporal.ZonedDateTime` 等を型安全に利用可能
- **RegExp.escape**: 正規表現の特殊文字を安全にエスケープする `RegExp.escape()` の型定義を追加（Stage 4）
- **Map の upsert メソッド**: `Map.prototype.getOrInsert()` と `Map.prototype.getOrInsertComputed()` の型定義を追加

### ジェネリック関数式の型チェック調整

ジェネリック呼び出し内の関数式、特にジェネリック JSX 式での型チェックが調整された。これは TypeScript 7.0（Go ベース）との挙動統一を目的としている。

## 破壊的変更・移行ガイド

### 非推奨化されたオプション

以下のオプションが非推奨となった。将来のバージョンで削除予定:

- **`target: es5`** — モダンブラウザを対象とするプロジェクトでは不要
- **`--moduleResolution node`** — `nodenext` または `bundler` への移行を推奨
- **`baseUrl`**（パスマッピング以外の用途）
- **`amd`、`umd` モジュール形式**
- **`outFile` オプション**

### 移行のポイント

1. **`strict: true` の影響確認**: これまで明示的に `strict: true` を指定していなかったプロジェクトは、型エラーが新たに発生する可能性がある。`strict: false` を明示するか、エラーを順次修正する
2. **`types: []` の影響確認**: `@types/node` 等を利用している場合、`tsconfig.json` の `types` に明示的に列挙する必要がある
3. **`moduleResolution` の移行**: `node` を使用している場合、`nodenext`（Node.js 向け）または `bundler`（バンドラー利用時）に切り替える

```jsonc
// tsconfig.json の推奨設定例（TypeScript 6.0）
{
  "compilerOptions": {
    // 6.0 のデフォルトで問題ない場合は省略可能
    "strict": true,           // デフォルト
    "target": "es2025",       // デフォルト
    "module": "esnext",       // デフォルト
    "moduleResolution": "bundler",  // 明示推奨
    "types": ["node"]         // 必要な型を明示
  }
}
```

## 今後の注目点

- **TypeScript 7.0**（2026年中盤予定）: Go ベースのコンパイラへ移行。並列処理対応により大規模プロジェクトでのコンパイル速度が劇的に向上する見込み
- **プラグインエコシステムへの影響**: 7.0 でのコンパイラアーキテクチャ変更により、既存の TypeScript プラグインや Language Service Plugin の互換性に注意が必要
- **6.0 → 7.0 の移行パス**: 6.0 で非推奨化されたオプションは 7.0 で削除される可能性が高いため、早めの対応を推奨
