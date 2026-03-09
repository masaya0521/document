# TypeScript 6.0 RC — JS ベース最後のメジャーリリース

- **日付**: 2026-03-06
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/03/06/typescript-6-0-rc-bridges-to-go-based-future.aspx)

## 概要

TypeScript 6.0 RC が 2026 年 3 月 6 日にリリースされた。JavaScript（セルフホスト）で書かれた TypeScript コンパイラとしては最後のメジャーリリースとなり、次の TypeScript 7.0 は Go 言語で再実装されたネイティブコンパイラ（Project Corsa）に移行する。6.0 はその橋渡しとなるリリースであり、多数のデフォルト値変更と非推奨化によって、7.0 への移行コストを最小限に抑えることを目指している。

## 主な変更点

### デフォルト値の大幅変更

最も影響が大きいのはコンパイラオプションのデフォルト値変更。既存プロジェクトで明示的に設定していない場合、挙動が変わる可能性がある。

| オプション | 旧デフォルト | 新デフォルト |
|-----------|------------|------------|
| `strict` | `false` | **`true`** |
| `module` | `commonjs` | **`esnext`** |
| `target` | 古いバージョン | **`es2025`** |
| `types` | 自動検出（@types 全取得） | **`[]`（空配列）** |

`types` が空配列になることで、ビルド時間が 20-50% 改善されるケースがテストで確認されている。

### ES5 サポートの廃止

最小ターゲットが **ES2015** に引き上げられた。`target: es5` は非推奨となり、以下の関連オプションも廃止:

- `--downlevelIteration`
- `--importHelpers`（ES5 向けのヘルパー関連）

### モジュール解決の整理

レガシーなモジュール関連オプションが大量に非推奨化:

- `--moduleResolution node`（node10）→ `node16` または `bundler` を使用
- `--moduleResolution classic` → 廃止
- `--module amd/umd/systemjs/none` → 廃止
- `--baseUrl` → `paths` に統合
- `--outFile` → 廃止
- `import assertions`（`assert` キーワード）→ `import attributes`（`with` キーワード）に移行

### 強制されるオプション

- `esModuleInterop`: **常に `true`**（設定不可）
- `allowSyntheticDefaultImports`: **常に `true`**
- `alwaysStrict`: 廃止（strict モードは常に有効）

### 新機能

- **`this` を使わない関数の型推論改善**: メソッド構文の関数でも `this` を使わない場合、アロー関数と同等の型推論が機能
- **サブパスインポートの拡張**: `#/` で始まるインポートをサポート（Node.js 仕様に準拠）
- **Temporal API の型定義**: ステージ 3 の Temporal API を組み込み型として提供
- **`RegExp.escape`**: ES2025 で追加された正規表現エスケープメソッドの型を追加
- **Map/WeakMap の `getOrInsert`/`getOrInsertComputed`**: upsert パターンをサポート
- **DOM 型の統合**: `lib.dom.iterable` と `lib.dom.asynciterable` を `lib.dom` に統合

### TypeScript 7.0 移行支援

- **`--stableTypeOrdering` フラグ**: 7.0（Go ベース）との型の順序の互換性を確保。最大 25% の性能低下があるが、移行時の差分確認に有用
- **`ignoreDeprecations: "6.0"`**: 非推奨警告を一時的に抑制可能（7.0 では削除される）

## 破壊的変更・移行ガイド

### 必須の対応

1. **`types` フィールドの明示指定**
   ```json
   {
     "compilerOptions": {
       "types": ["node", "jest"]
     }
   }
   ```
   デフォルトが空配列に変わるため、必要な型定義を明示的に列挙する。

2. **`module` と `moduleResolution` の更新**
   ```json
   {
     "compilerOptions": {
       "module": "node16",
       "moduleResolution": "node16"
     }
   }
   ```
   または Vite/webpack 等のバンドラーを使っている場合:
   ```json
   {
     "compilerOptions": {
       "module": "esnext",
       "moduleResolution": "bundler"
     }
   }
   ```

3. **`baseUrl` から `paths` への移行**
   ```json
   // Before
   { "baseUrl": "./src" }

   // After
   {
     "paths": {
       "@/*": ["./src/*"]
     }
   }
   ```

4. **ES5 ターゲットの撤廃対応**
   - IE11 等のレガシーブラウザサポートが不要な場合は対応不要
   - 必要な場合は Babel 等の外部トランスパイラを使用

### 段階的な移行戦略

TypeScript チームは以下の段階的アプローチを推奨:

1. まず 6.0 RC にアップグレード
2. `ignoreDeprecations: "6.0"` で非推奨警告を一時抑制
3. 非推奨オプションを順次置き換え
4. `--stableTypeOrdering` で 7.0 との互換性を確認
5. 7.0 リリース時にスムーズに移行

## 今後の注目点

- **TypeScript 7.0**（2026 年夏予定）: Go ベースのネイティブコンパイラで 5-10x のコンパイル速度向上、約 8x のエディタ起動改善、約 50% のメモリ削減が見込まれる
- **6.0 GA**: RC から大きな変更なく近日中にリリース予定
- **エコシステムの対応**: 主要フレームワーク（Next.js, Angular 等）の TS 6.0 対応状況を確認する必要がある
- **`ignoreDeprecations` の期限**: 7.0 で完全削除されるため、6.0 の間に非推奨オプションの置き換えを完了しておくことが重要
