# Google I/O 2026: Gemini 3.5 Flash と Antigravity 2.0 の意味

- **日付**: 2026-05-21
- **カテゴリ**: Tech
- **ソース**: [Google Developers Blog](https://developers.googleblog.com/all-the-news-from-the-google-io-2026-developer-keynote/) / [9to5Google](https://9to5google.com/2026/05/19/google-io-2026-news/) / [HotHardware](https://hothardware.com/news/google-io-2026-gemini-35-flash-ai-search-and-more)

## 概要

Google I/O 2026 のキーノートで、Gemini 3.5 Flash が即日 GA となり、上位モデルの Gemini 3.5 Pro は来月リリースが予告された。同時に、エージェントファースト型の開発プラットフォーム「Antigravity」が 2.0 へ大型アップデート、AI Studio には Kotlin (Android) ネイティブサポートと Cloud Run へのワンクリックデプロイが追加された。Google は「AI が補助するフェーズ」から「エージェントが自律的にタスクを完遂するフェーズ」への明確な転換を打ち出した。

「マルチモデル戦略」と「エージェント開発基盤」を同時に進めるこの構成は、競合の OpenAI／Anthropic が個別プロダクトで提示してきたエージェント体験を、Google が IDE・モバイル・Search・Workspace へ統合的に展開できるという独自の強みを浮き彫りにする発表となった。

## 詳細

### Gemini 3.5 Flash の位置づけ

- フロンティア級の知能を保持したまま、競合フロンティアモデルと比べて **出力トークン生成速度が約 4 倍**。
- 価格は **$1.50 / $9 per 1M tokens（入力/出力）**、コンテキスト長は **1M tokens**。
- 内部ベンチマークで旧 Gemini 3.1 Pro を全般に上回り、特にコーディング・エージェント・マルチモーダルで顕著な向上。
- 「Flash」が Pro 級の質と価格優位を両立した点は、エージェント運用（多数の小ステップ）のコスト構造を一気に押し下げる可能性が高い。

### Gemini 3.5 Pro と Gemini Omni

- Gemini 3.5 Pro は社内テスト中で、来月リリース予定。今回の I/O では Flash 単独 GA に絞り、Pro はティザー扱い。
- **Gemini Omni** は「任意の入力から任意の出力を生成する」モデルファミリーで、Veo（動画）や Nano Banana（画像）系の生成モデルと Gemini 知能を統合。物理（重力・運動）のシミュレーション精度が大幅向上。
- 最初の派生モデル **Gemini Omni Flash** が同日に Gemini アプリで提供開始。

### Antigravity 2.0 と AI Studio の進化

- Antigravity は「Agent-first 開発プラットフォーム」と再定義され、エージェントが IDE 内で長い依存関係チェーンのタスクを処理する設計。
- AI Studio から **ワンクリックで Antigravity にエクスポート**できるようになり、プロトタイプ→エージェント実装の摩擦が大きく低下。
- AI Studio に **Kotlin（Android）ネイティブサポート** と Google Workspace 連携、Cloud Run へのワンクリックデプロイが追加。フルスタックアプリを AI Studio 内で構築可能に。

### エージェント体験のプロダクト浸透

- Search・Android・Workspace の各面で「エージェントが自律的に複雑タスクを完遂する」機能群が公開。
- AI Glasses（秋ローンチ）と Android XR の話題も並走しており、エージェント体験をデバイスへ拡張する方針を強調。

## 今後の注目点

- Gemini 3.5 Pro の実ベンチマークと、対 Claude Opus 4.7／GPT-5 系との比較。特にコーディング系の Antigravity 連動性能。
- Antigravity 2.0 が VS Code 拡張や Cursor などの既存エージェント IDE のユーザーシェアにどう食い込むか。
- Gemini Omni Flash の物理シミュレーション能力が、ロボティクス／3D／ゲーム生成ワークフローへ実用展開するか。
- Flash 系の価格優位がエージェント運用コストに与える影響（OpenAI Codex / Anthropic の API 価格戦略への波及）。
- AI Glasses ローンチ時の Gemini 統合度、Android XR の開発者エコシステム拡大状況。
