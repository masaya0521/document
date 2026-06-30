# TypeScript — 7.0 RC（Go ネイティブコンパイラ）

- **日付**: 2026-07-01（RC は 2026-06-18 公開）
- **カテゴリ**: Language / Build Tool
- **ソース**: [Announcing TypeScript 7.0 RC](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-rc/), [Announcing TypeScript 7.0 Beta](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/)

## 概要

TypeScript チームは、コンパイラ／ツールチェーンを Go 言語へ全面移植した「Project Corsa」を、2026-06-18 に Release Candidate へ到達させた。2026-04-21 の Beta に続くもので、GA（正式版）は RC から約1ヶ月以内、すなわち 7月中〜下旬が見込まれている。

最大の特徴は型チェック性能で、ネイティブコードの実行速度と共有メモリ並列化の組み合わせにより、TypeScript 6.0 比でおおむね約10倍の高速化を実現する。大規模コードベースでのコンパイル時間短縮、エディタ起動の高速化、メモリ使用量の大幅削減（約50%）が報告されている。重要なのは、既存実装を一から書き直したのではなく、型チェックロジックを構造的に同一なまま Go へ「移植」した点であり、6.0 との互換性が重視されている。

## 主な変更点

- **Go への移植**: TypeScript（自己ホスト型の JS 出力コードベース）から Go へ移植。ネイティブバイナリ `tsgo` として配布
- **約10倍の高速化**: 大規模コードベースでコンパイル時間が最大10倍改善、メモリ使用量も大幅削減
- **並列処理フラグ**: 新しい `--checkers` / `--builders` フラグで型チェックとプロジェクトビルドを並列実行可能
- **ウォッチモード刷新**: Parcel のファイルウォッチャーをベースに再構築
- **Unicode 処理改善**: テンプレートリテラル型で Unicode コードポイントを自然に保持
- **JavaScript サポート見直し**: JSDoc の特殊な扱いを削減し、TypeScript 解析との一貫性を向上

## 破壊的変更・移行ガイド

- 型チェックロジックは 6.0 と構造的に同一で、`stableTypeOrdering` や `ignoreDeprecations` などの条件下で互換性が維持される
- ネイティブ移植に伴い、コンパイラ内部 API（カスタムトランスフォーマー等）に依存するツールは影響を受ける可能性があるため、`tsgo` 上での動作確認が必要
- 既存プロジェクトはまず RC を CI に並走させ、型エラーの差分・ビルド成果物の同一性を検証してから切り替えるのが安全

## 今後の注目点

- GA リリース（RC から約1ヶ月以内予定）のタイミングと、エコシステム（ESLint、ts-node、各種ビルドツール）の `tsgo` 対応状況
- Visual Studio 2026 / VS Code での既定有効化の進行度
- コンパイラ内部 API に依存する周辺ツールの追従と、移行に伴う非互換の洗い出し
