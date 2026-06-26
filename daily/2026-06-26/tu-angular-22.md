# Angular — v22 リリース

- **日付**: 2026-06-03
- **カテゴリ**: Frontend
- **ソース**: [Angular 公式ブログ](https://blog.angular.dev/), [Angular 22: The Most Important New Features at a Glance（ANGULARarchitects）](https://www.angulararchitects.io/en/blog/angular-22-the-most-important-new-features-at-a-glance/), [Angular 22: Key Features and Changes（Angular.love）](https://angular.love/angular-22-key-features-and-changes)

## 概要

Angular v22 が 2026 年 6 月 3 日にリリースされた。v21（2025/11）で実験的・開発者プレビューとして導入された主要機能が一斉に安定化し、「Signal-First（シグナルファースト）」のアーキテクチャが本格的に実用段階へ到達したメジャーリリースである。Signals を中核に据えたフォーム・リソース取得・変更検知の刷新が一通り揃い、Zone.js への依存を前提としない開発スタイルがデフォルトに近づいた。

## 主な変更点

### Selectorless Components（セレクタレスコンポーネント）

- セレクタ文字列を定義せず、テンプレート内にコンポーネントを直接 import して利用できる。
- リファクタリング耐性の向上、名前衝突の回避、大規模コードベースでのコンポーネント利用時の型安全性向上が狙い。

### Signal Forms の安定化

- v21 で実験的に導入された Signal ベースのフォームシステムが stable に到達。
- Submission API、`validateStandardSchema` による動的スキーマ、条件付き CSS クラス、既存 Reactive Forms との相互運用（interop）を備え、本番投入可能なフォームスタックとして整備された。

### その他の安定化・デフォルト変更

- **Resource API**（`resource` / `rxResource` / `httpResource`）が安定化。
- **Angular ARIA** のヘッドレスコンポーネント群（アコーディオン、コンボボックス、グリッド、リストボックス、メニュー、タブ、ツールバー、ツリー等）が安定化。
- **MCP server** が安定化し、Angular CLI が AI 支援開発向けの Model Context Protocol を標準サポート。
- **OnPush** が新規プロジェクトのデフォルト変更検知戦略に。
- **Incremental Hydration**（増分ハイドレーション）がデフォルトで有効化。

## 破壊的変更・移行ガイド

- OnPush デフォルト化や Zoneless 化の流れにより、変更検知に暗黙的に依存していたコンポーネントの挙動を確認する必要がある。
- Reactive Forms から Signal Forms への移行は interop が用意されているため段階的に進められるが、新規実装では Signal Forms を前提に設計するのが推奨される。
- `ng update` による自動マイグレーションを利用し、公式の Update Guide で対象バージョン間の差分を確認すること。

## 今後の注目点

- Signals を中心とした API の収斂がさらに進み、従来の RxJS 主体のパターンとの棲み分け・移行指針がエコシステム全体でどう固まるか。
- Selectorless Components の普及により、コンポーネントモジュール設計・ライブラリ配布の慣習がどう変化するか。
- MCP server 安定化を起点とした AI 支援開発ツールチェーンの広がり。
