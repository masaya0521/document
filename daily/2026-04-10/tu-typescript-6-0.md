# TypeScript 6.0 — JavaScript ベース最後のリリースと v7.0 への移行準備

- **日付**: 2026-03-23
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/03/23/typescript-6-0-ships-as-final-javascript-based-release-clears-path-for-go-native-7-0.aspx)

## 概要

TypeScript 6.0 は、現行の JavaScript ベースコンパイラにおける最後のメジャーリリースである。Go 言語で再実装される TypeScript 7.0 への「橋渡し」として位置づけられ、多くのデフォルト値変更と非推奨化が行われた。開発者は 6.0 の移行を通じて、7.0 で予定されている破壊的変更に段階的に備えることができる。

## 主な変更点

### 新機能

- **Temporal API 型定義**: ステージ4に到達した Temporal API の型定義を搭載
- **Map/WeakMap の `getOrInsert` メソッド**: コレクション操作の簡素化
- **`RegExp.escape` 型サポート**: es2025 ターゲットで利用可能
- **`dom.iterable` の統合**: DOM 型に iterable サポートを統合
- **`#/` サブパスインポート**: Node.js のサブパスインポートに対応
- **`--moduleResolution bundler` と `--module commonjs` の組み合わせ**: より柔軟なモジュール設定
- **型推論の改善**: `this` を使用しないメソッド構文の関数を文脈敏感性から除外し、ジェネリック呼び出し内の型推論が向上

### デフォルト値の変更

| オプション | 旧デフォルト | 新デフォルト |
|-----------|-------------|-------------|
| `strict` | `false` | `true` |
| `module` | `commonjs` | `esnext` |
| `target` | `es3` | `es2025` |
| `types` | 全自動読み込み | `[]`（明示的指定が必要） |

### TypeScript 7.0 への移行支援

- **`--stableTypeOrdering` フラグ**: 型順序を安定化し、Go ベースコンパイラとの互換性を検証可能

## 破壊的変更・移行ガイド

### 非推奨化された機能（7.0 で削除予定）

- `target: "es5"` — モダンブラウザ / Node.js 環境では不要
- `--downlevelIteration` — ES5 ターゲット廃止に伴い不要
- `--moduleResolution node` — `node16` または `bundler` に移行
- `--baseUrl` — パスマッピングには `paths` を使用
- AMD / UMD / SystemJS モジュール形式

### 移行手順

1. **`tsconfig.json` を確認**: デフォルト値の変更により、既存プロジェクトの動作が変わる可能性がある
2. **非推奨警告を確認**: コンパイラ出力の deprecation 警告を確認し、該当箇所を修正
3. **一時的な抑制**: `"ignoreDeprecations": "6.0"` を設定することで非推奨警告を一時的に抑制可能（7.0 では無効）
4. **`--stableTypeOrdering` で検証**: Go ベースコンパイラとの互換性を事前に確認

## 今後の注目点

- **TypeScript 7.0**: Go 言語で再実装されたコンパイラ。マルチスレッド対応による大幅なパフォーマンス向上が期待される（2026年中盤リリース予定）
- **ネイティブプレビュー版**: npm で `@typescript/native-preview` として既に提供中。早期検証が可能
- **6.0 で非推奨化された機能の完全削除**: 7.0 では `ignoreDeprecations` による抑制も無効化
- **エディタサポート**: WebStorm 2026.1 が TypeScript 6.0 の新しいデフォルトに対応済み。VS Code も Language Service 経由で対応
