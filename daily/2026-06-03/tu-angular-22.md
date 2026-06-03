# Angular — v22「Signal-First」メジャーリリース

- **日付**: 2026-06-03（2026-06-03 週に GA 予定 / RC.1 は 2026-05-20）
- **カテゴリ**: Frontend
- **ソース**: [angular/angular Releases](https://github.com/angular/angular/releases), [angular.dev リリースポリシー](https://angular.dev/reference/releases)

## 概要

Angular 22 は、過去 2 年間にわたって実験的に投入されてきた Signal ベースの機能群を「安定版の標準」へと昇格させる、近年で最も重要なメジャーリリースと位置づけられている。半年ごとのリリースサイクルに沿って 2026 年 6 月初週に GA が予定されており、目玉は **Signal Forms の安定化** と **selectorless components**、そして **zoneless アーキテクチャの本格化** である。

これまで RxJS と Zone.js に依存していた変更検知・状態管理を、きめ細かい（fine-grained）リアクティビティを持つ Signal に置き換える方向性が明確になり、コンポーネントツリー全体の検査から「依存しているコンポーネントだけを更新する」モデルへ移行する。ボイラープレートの削減・パフォーマンス向上・AI 支援ツールとの親和性向上を一貫したテーマとしている。

## 主な変更点

- **Signal Forms の安定化**: v21 で実験段階だった Signal ベースのフォームが production-stable に。リアクティブフォームの定型コードを大幅に削減する。
- **selectorless components**: これまで必須だった CSS セレクターなしで、テンプレートにコンポーネントクラスを直接 import して利用できる。
- **zoneless アーキテクチャ**: Zone.js への依存を外した変更検知が安定化。グローバルな常時監視を排し CPU サイクルを削減する。
- **OnPush をデフォルト化**: 新規コンポーネントの `ChangeDetectionStrategy` が OnPush 基準となり、signals-first / zoneless 方針と整合する。
- **Vitest による高速テスト**: テストランナーとして Vitest をサポートし、ユニットテストの実行が高速化。
- **MCP サポート**: Angular CLI が Model Context Protocol を標準サポートし、AI コーディングアシスタントがプロジェクト構造を理解しやすくなる。
- TypeScript 5.9 サポート、incremental hydration、resource API、tree-shaking 改善なども含む。

## 破壊的変更・移行ガイド

- **OnPush のデフォルト化**: 新規コンポーネントの変更検知戦略が変わるため、暗黙的に Default 戦略へ依存していたコードは挙動差に注意。既存コンポーネントは明示指定が優先されるため影響は限定的。
- **zoneless 前提への移行**: Zone.js のパッチ挙動（`setTimeout` 後の自動変更検知など）に暗黙依存している箇所は、signals / `markForCheck` への置き換えが必要になる場合がある。
- `ng update` による自動マイグレーションが提供される見込み。実験フラグで利用していた Signal Forms / selectorless は安定版 API への追従を確認すること。

## 今後の注目点

- Signal Forms の安定化に伴い、テンプレート駆動 / リアクティブフォームに続く「第三の選択肢」がエコシステムにどう浸透するか。
- selectorless components がコミュニティのコンポーネントライブラリ設計に与える影響。
- MCP サポートを起点とした AI 支援開発（vibe coding）ワークフローの広がり。
