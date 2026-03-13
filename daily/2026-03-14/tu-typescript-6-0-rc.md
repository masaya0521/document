# TypeScript 6.0 RC — Go ベースへの橋渡しリリース

- **日付**: 2026-03-06
- **カテゴリ**: Language
- **ソース**: [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/), [InfoWorld](https://www.infoworld.com/article/4143186/typescript-6-0-reaches-release-candidate-stage.html)

## 概要

TypeScript 6.0 RC は、現行の JavaScript ベースコンパイラとしては最後のメジャーリリースとなる。次期 TypeScript 7.0 は Go 言語で書き直された新しいコンパイラ・言語サービスを基盤とするため、6.0 は 5.x 系から 7.0 への橋渡し的な位置づけとなる。6.0 はフィーチャーフリーズ済みで、今後はクリティカルなバグ修正のみが予定されている。

## 主な変更点

### RegExp.escape

ECMAScript の Stage 4 提案に基づく `RegExp.escape()` 関数をサポート。正規表現の特殊文字を安全にエスケープできる。

### ES2025 サポート

`target` および `lib` オプションで `es2025` を指定可能に。

### --stableTypeOrdering フラグ

新しい `--stableTypeOrdering` フラグにより、型の出力順序を TypeScript 7.0 と一致させることができる。7.0 への移行準備として有用。

### サブパスインポートのサポート

`#/` で始まるサブパスインポート（package.json の `imports` フィールド）をサポート。

### --moduleResolution bundler と --module commonjs の組み合わせ

これまで組み合わせられなかった `--moduleResolution bundler` と `--module commonjs` を同時に使用可能に。

### ジェネリック呼び出しにおける関数式の型チェック改善

ジェネリックな JSX 式内での関数式に対する型チェックが改善された。

### import assertion 構文の非推奨拡大

`import()` 呼び出しにおいても import assertion 構文（`assert`）が非推奨に。`with` 構文への移行が推奨される。

### DOM 型の更新

最新の Web 標準に合わせて DOM 型が更新。Temporal API 関連の型も調整された。

## 破壊的変更・移行ガイド

TypeScript 6.0 自体の破壊的変更は比較的少ないが、7.0 への移行を見据えた準備が重要：

1. **`--stableTypeOrdering` を有効にしてテスト**: 7.0 での型順序変更による影響を事前に確認
2. **import assertion → import attributes への移行**: `assert` を `with` に書き換え
3. **CI で 6.0 RC を試す**: 6.0 は 5.x からの自然なアップグレードパスを提供

```typescript
// Before (deprecated)
import data from "./data.json" assert { type: "json" };

// After (recommended)
import data from "./data.json" with { type: "json" };
```

## 今後の注目点

- **TypeScript 7.0**: Go で書き直された新コンパイラ。10 倍以上の高速化が見込まれる
- **エディタ統合**: 7.0 では言語サービスも Go ベースとなり、エディタの応答性が大幅に向上する見込み
- **移行ツール**: 6.0 → 7.0 の移行を支援するツールやガイドが今後提供される予定
- **プラグインエコシステム**: 7.0 のアーキテクチャ変更がサードパーティプラグインに与える影響に注意
