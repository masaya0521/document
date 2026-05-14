# Angular 22.0-rc.0 — Selectorless Components と Signal-first 時代の到来

- **日付**: 2026-05-15
- **カテゴリ**: Frontend
- **ソース**: [Angular v21 / v22 Event Page](https://angular.dev/events/v21), [Medium (Angular Engineering)](https://medium.com/angular-engineering/angular-22-the-shift-to-signal-first-zoneless-and-performance-driven-architecture-b0d5a68f51e6), [VersionLog](https://versionlog.com/angular/22.0/), [HeroDevs](https://www.herodevs.com/blog-posts/angular-version-history-every-release-date-support-window-and-end-of-life-date-from-angularjs-to-angular-22)

## 概要

Angular 22.0-rc.0 が 2026-05-13 に公開された。Angular 21（2025-11）で「Signals が正式に基盤に組み込まれた最初のリリース」だったのに対し、22 は **Signals / Zoneless / 新しい Forms / Selectorless** という長年の構想が一気に “標準” として揃う節目のメジャー。「Signal-first 時代の到来」と位置付けられている。

正式 GA は 2026 年 5 月後半の予定で、RC からの追加の挙動変更は最小限にとどまる見込み。

## 主な変更点

### Selectorless Components

これまで Angular は文字列セレクタ（`app-foo` のような）で他コンポーネントをテンプレートから参照する仕組みだったが、22 では **テンプレート内でコンポーネントクラスを直接 `import` して使える** ようになる。

```ts
// Selectorless: クラスを直接テンプレートに import
import { UserCard } from './user-card';

@Component({
  template: `
    <UserCard [user]="user" />
  `,
})
export class ProfilePage {}
```

メリット:

- **リファクタリングが圧倒的に楽**: クラス名を変えれば呼び出し側もエディタが自動追従
- **型安全性**: セレクタ文字列に頼らないので IDE / コンパイラがミスを即座に検出
- **命名衝突の解消**: 大規模コードベースで `app-` プレフィックスを延々と気にする必要がなくなる
- **モジュール認知負荷の低減**: 「このセレクタはどのクラス？」を覚えなくてよくなる

### Signal-based Forms の正式安定化

21 で実験的に入った Signal-based Forms が 22 で **正式に stable** になる。従来の Reactive Forms に対して以下が変わる:

- **Fine-grained updates**: 50 フィールドの巨大フォームでも、変更のあったフィールドだけが更新される。フォームツリー全体の再評価が走らない
- **Zoneless との親和性**: zone.js を介さない変更検知と自然に噛み合う
- **Signal による validation / state / two-way binding**: シグナル同士の合成で書ける

### Zoneless がデフォルトに

`zone.js` への依存を排した **Zoneless モードが新規プロジェクトのデフォルト** に。

- バックグラウンドでクリックやタイマーを片っ端からトラックする必要がなくなり、バンドルサイズと実行コストが軽くなる
- 新規コンポーネントは `OnPush` 相当が前提のコーディングスタイルが推奨される
- 既存アプリは引き続き `zone.js` を有効化して段階的に移行可能

### Vitest がデフォルトテストランナー

Angular CLI が **Vitest を新規プロジェクトの既定テストランナー** に採用。Karma + Jasmine からの脱却が CLI レベルで整う。既存プロジェクトは Karma を継続利用できる。

### TypeScript 5.9 サポート

22 は **TypeScript 5.9 を要求**。21.x が許容していた古い TS バージョンは外れる。

## 破壊的変更・移行ガイド

主な互換性ポイント:

- **TypeScript 5.9 へのアップグレードが必須**。`tsconfig.json` の `strict` 系設定はそのままで通るが、ライブラリ側の依存も TS 5.9 互換にする必要がある
- **Angular 19 が 2026-05 で EOL**: 19 系アプリは 20 以上へ移行しないとセキュリティ修正を受けられなくなる
- **Zoneless 化**: 既存アプリは強制ではないが、新規 `OnPush` 既定 + Signal 推奨という方向性に追随しないと、Angular 23+ で徐々に苦しくなる
- **Forms 移行**: Reactive Forms から Signal-based Forms への切り替えは強制ではない。共存可能。新規フォームから順次採用するのが現実的
- **Selectorless**: 既存のセレクタベースの記述はそのまま動くので、新規コンポーネントから採用する形で段階移行できる

## 今後の注目点

- **Angular 22 GA タイミング**: 2026-05 後半に GA 予定。RC.0 から RC.x を経てフィックスが入る
- **エコシステムの追従**: PrimeNG / Material 等の主要 UI ライブラリが Selectorless と Signal Forms をどれだけ早く本格対応するか
- **Vitest 既定化の影響**: テストランナー切替に伴う既存スナップショット・モックライブラリの互換性
- **Zoneless が当たり前になる時代の DevTools / Profiler**: zone.js を前提とした既存トラッキングツールの再設計
- **Selectorless の lint / フォーマット**: 命名規則をどう揃えるか、自動 import の運用がチームでどう定着するか
