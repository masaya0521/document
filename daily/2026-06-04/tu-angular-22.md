# Angular 22 — Signal-First 時代の到来

- **日付**: 2026-06-04（22.0.0-rc.1 は 2026-05-20）
- **カテゴリ**: Frontend
- **ソース**: [HeroDevs — Angular Version History](https://www.herodevs.com/blog-posts/angular-version-history-every-release-date-support-window-and-end-of-life-date-from-angularjs-to-angular-22), [VersionLog — Angular 22.0](https://versionlog.com/angular/22.0/)

## 概要

Angular 22 は、6 か月ごとのメジャーリリースサイクルに沿って 2026 年 5 月に登場した（22.0.0-rc.1 が 5/20 公開）。Signals を中核に据えた「Signal-First」アーキテクチャを推し進め、過去数年で最も重要なリリースと位置づけられている。Zoneless 化・OnPush デフォルト化・Signal Forms 安定化が揃い、コンポーネントの書き方そのものが変わる。

## 主な変更点

- **Selectorless Components**: 文字列セレクタの定義・記憶が不要になり、コンポーネントをテンプレートへ直接 import して利用可能。リファクタリング耐性と型安全性が向上。
- **Signal Forms の安定化**: Angular 21 で実験的に導入された Signal Forms が成熟し、推奨フォーム管理 API に近づく（あるいは stable 化）。
- **OnPush をデフォルトに**: 新規コンポーネントで `ChangeDetectionStrategy.OnPush` がデフォルトとなり、zoneless / signals-first 路線に整合。
- **TypeScript 5.9 対応**: 最新の型チェック改善を取り込み。
- **テスト・SSR・MCP**: Vitest によるテスト高速化、SSR 改善、AI ツール連携のための Angular MCP Server への継続投資。

## 破壊的変更・移行ガイド

- 新規コンポーネントの OnPush デフォルト化により、ミューテーション前提で変更検知に依存していたコードは挙動が変わる可能性がある。`signal()` ベースの状態管理への移行を推奨。
- selectorless への移行は段階的に可能だが、既存のセレクタ前提のテンプレート／テストは順次見直しが必要。
- `ng update` による自動マイグレーションを基本とし、Signal Forms 採用は新規フォームから段階導入するのが安全。

## 今後の注目点

- Signals / Zoneless / OnPush が production-stable に揃ったことで、RxJS 中心の従来パターンからの移行ガイドラインが今後の焦点。
- selectorless の普及度と、周辺ツール（Angular Language Service、各種 UI ライブラリ）の追従状況。
- MCP Server を介した AI 支援開発の実用度。
