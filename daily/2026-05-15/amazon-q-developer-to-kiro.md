# Amazon Q Developer から Kiro への移行：AWS 開発者ツールの再編

- **日付**: 2026-05-15
- **カテゴリ**: Tech
- **ソース**:
  - [AWS DevOps Blog — Amazon Q Developer end-of-support announcement](https://aws.amazon.com/blogs/devops/amazon-q-developer-end-of-support-announcement/)
  - [Kiro Docs — Migrating from Amazon Q Developer](https://kiro.dev/docs/migrating-from-q-developer/)
  - [DEV.to — Amazon Kiro: The Spec-Driven AI IDE Replacing Amazon Q](https://dev.to/austriasoftwaroftwaredeveloper/amazon-kiro-the-spec-driven-ai-ide-replacing-amazon-q-2f5f)

## 概要

AWS は Amazon Q Developer の IDE プラグインと有償サブスクリプションを段階的に終了し、後継製品 **Kiro** に統合する EOS（End-of-Support）スケジュールを公表した。本日 2026-05-15 から新規サインアップが停止され、最終 EOS は 2027-04-30。Opus 4.7 を含む最新コーディングモデルは Kiro 専用となるため、Q Developer 利用者は実質的に 1 年以内の移行を迫られる。

これは AWS の AI 開発者ツール戦略の大きな転換であり、Cursor / Cline / Claude Code といった Spec-Driven な AI IDE 競合に対抗するための再編と位置付けられる。

## 詳細

### EOS タイムライン

| 日付 | 事象 |
|------|------|
| **2026-05-15** | Amazon Q Developer の **新規サインアップ停止**。既存契約は継続でユーザー追加可。 |
| **2026-05-29** | Q Developer Pro 上の **Opus 4.6 利用終了**。Opus 4.5 と既存モデルは継続利用可だが、**最新モデル（Opus 4.7 など）は Kiro 専用**。 |
| **〜2027-04-30** | この間、重要な不具合修正は継続。新機能開発は Kiro 側に集中。 |
| **2027-04-30** | **IDE プラグインと有償サブスクリプションが完全 EOS**。 |

ただし、AWS Management Console、AWS Marketing Site、AWS Documentation Site、AWS Console Mobile App、Slack/Teams 向け Amazon Q Developer for Chat Apps など、AWS 自社サービスに統合された Q Developer 機能は **EOS 対象外**で継続提供される。

### Kiro とは

Kiro は AWS が "Spec-Driven AI IDE" として位置付ける後継製品。Amazon Q Developer がチャット中心のコード補完アシスタントだったのに対し、Kiro は

- **Spec（仕様）から実装を生成するワークフロー**
- 最新の Anthropic Claude モデル（Opus 4.7 含む）の専有提供
- ファイル横断のリファクタや複数ステップのタスク実行に最適化

を売りにしている。Cursor が "AI ペアプログラマー" を、Claude Code が "ターミナル中心の AI エージェント" を志向しているのに対し、Kiro は「設計駆動」を差別化軸にしている。

### なぜ Q Developer を捨てて Kiro なのか

3 つの理由が考えられる:

1. **モデル更新サイクルの差**
   Q Developer は AWS の社内承認とライフサイクル管理に縛られ、Anthropic 最新モデルへの追従が遅れがちだった。Kiro として再ブランディングし、最新モデルを優先投入できる体制に切り替えた。

2. **製品コンセプトの矛盾解消**
   Q Developer は「AWS リソース管理 + コード生成 + チャット」を一手に担っていたため、UX が肥大化していた。Spec-Driven の純粋な IDE 機能を Kiro に分離し、AWS リソース管理用の Q は Console 等に残す形で責務を整理した。

3. **競合製品（Cursor、Claude Code、Cline）への対抗**
   2025-2026 年に AI IDE 市場の競争が激化し、Q Developer のチャット中心 UI では機能差別化が難しくなった。Spec-Driven という軸で再起動する戦略。

### 既存ユーザーへの影響

- **個人開発者**: 12 ヶ月の移行猶予がある。Opus 4.7 を使いたい場合は実質的に Kiro への乗り換えが必要。
- **エンタープライズ**: Eclipse ベースの IDE 統合を持つ大企業では移行コストが大きい。Zenn のレビュー記事で「Eclipse ベース企業の Q Developer EOS 対応戦略」がすでに議論されている。
- **AWS 統合機能のヘビーユーザー**: Console / Slack / Teams 統合は影響を受けないため、AWS 運用面の利用は継続できる。

### 移行のポイント

- ライセンス/サブスクリプション体系が変わるため、Q Developer Pro の年間契約者は更新タイミングと Kiro 課金モデルの突き合わせが必要
- Q Developer のチャット履歴・カスタムプロンプトを Kiro に持ち込む手段は限定的
- Kiro Docs に「Migrating from Q Developer」が用意されているが、Spec-Driven のワークフローへの慣れは別途必要

## 今後の注目点

- Kiro と Cursor / Claude Code / Cline 間のシェア競争（Spec-Driven が定着するか）
- Anthropic と AWS のモデル契約条件（独占的提供がいつまで続くか）
- AWS 内部での Q ブランドの今後（Console 側の Q は残るが、ブランドの混乱は避けられない）
- 既存 Q Developer の OSS プラグインや三者ツールチェインへの影響
- 2027 年 4 月以降の Eclipse / JetBrains 統合の継続性
