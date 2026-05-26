# TypeScript 7.0 Beta — Go 移植による10倍高速化の全貌

- **日付**: 2026-04-21（ベータリリース日）
- **カテゴリ**: Language / Build Tool
- **ソース**: [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/), [GitHub](https://github.com/microsoft/TypeScript)

## 概要

TypeScript 7.0 Beta は、1年以上かけて TypeScript のコンパイラ全体を Go に移植した "Project Corsa" の成果物。ネイティブコードの速度とメモリ共有による並列化により、**最大10倍の高速化**を実現している。VS Code のコードベース（150万行）のコンパイルが78秒から7.5秒に短縮される。安定版は2026年6-7月にリリース予定。

## 主な変更点

### Go への完全移植

既存の TypeScript コンパイラを Go に完全移植。型チェックロジックは TypeScript 6.0 と構造的に同一で、Bloomberg・Figma・Google など大規模企業環境でテスト済み。新しいコンパイラコマンドは `tsgo`。

### 並列化フラグ

```bash
# 型チェックワーカー数の制御（デフォルト: 4）
tsgo --checkers 8

# プロジェクト参照の並列ビルド
tsgo --builders 4

# シングルスレッドモード（デバッグ用）
tsgo --singleThreaded
```

### 新しいデフォルト設定

TypeScript 7.0 では複数のデフォルト値が変更される。

| 設定 | 旧デフォルト | 新デフォルト |
|------|-------------|-------------|
| `strict` | `false` | **`true`** |
| `module` | （ターゲットに依存） | **`esnext`** |
| `target` | `ES3` | **現在の安定 ECMAScript バージョン** |

### パフォーマンスベンチマーク

| プロジェクト | tsc (TS 6.0) | tsgo (TS 7.0) | 改善倍率 |
|-------------|-------------|--------------|---------|
| VS Code（150万行） | 78秒 | 7.5秒 | ~10x |
| 中規模プロジェクト | 概ね同様の比率 | — | 8-10x |

## 破壊的変更・移行ガイド

### 廃止される機能

- **ES5 ターゲット**: ES5 への出力サポートが廃止。レガシーブラウザ対応が必要な場合は TS 6.x を継続使用
- **`downlevelIteration`**: ES5 廃止に伴い不要に
- **AMD / UMD モジュール形式**: ESM への移行が必須
- **従来の `moduleResolution`**: `bundler` または `nodenext` を使用

### tsconfig.json の移行ポイント

```jsonc
// TS 7.0 向けの tsconfig.json 調整例
{
  "compilerOptions": {
    // rootDir を明示的に指定（tsconfig.json 外のファイル参照時）
    "rootDir": "./src",

    // 型定義の自動読み込みが変更 → 明示的に指定
    "types": ["node", "jest"],

    // module / target は新デフォルトで十分なケースが多い
    // 必要に応じて明示指定
    "module": "esnext",
    "target": "es2024"
  }
}
```

### JSDoc の厳格化

JavaScript ファイルでの JSDoc サポートがより厳密に。値から型への参照が不可、`@enum` 廃止、スタンドアロン `?` 非対応など、TypeScript の型システムへの統一が進む。

### 移行チェックリスト

1. **`strict: true`** がデフォルトになるため、既存の `strict: false` プロジェクトは明示的に設定
2. **`rootDir`** を明示的に指定（特にモノレポ構成）
3. **`types`** 配列で使用する型定義を明示
4. **ES5 ターゲット**を使用している場合は移行計画を策定
5. **AMD/UMD** モジュール形式からの移行
6. TS 6.0 と 7.0 の並行運用期間を設けて段階的に移行

## 今後の注目点

- **2026年6-7月**: TypeScript 7.0 安定版リリース予定
- **7.1 以降**: プログラマティック API の提供（ツール・エディタ向け）
- **エディタ対応**: VS Code は TypeScript 7.0 Beta を VS 2026 18.6 Insiders で既にデフォルト有効化
- **エコシステム移行**: 主要フレームワーク（Next.js, Nuxt, Angular 等）の対応状況をウォッチ
- **TypeScript 6.x**: 安定版として引き続きサポートされるため、急ぎの移行は不要
