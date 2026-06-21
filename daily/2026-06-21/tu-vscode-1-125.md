# Visual Studio Code — v1.125（June 2026）

- **日付**: 2026-06-21
- **カテゴリ**: Dev Tool
- **ソース**: [Release Notes v1.125](https://code.visualstudio.com/updates/v1_125), [Releasebot](https://releasebot.io/updates/microsoft/visual-studio-code)

## 概要

VS Code 1.125（2026 年 6 月 17 日リリース）は、エディタに統合されたブラウザの実用性向上、AI モデルプロバイダのインストール導線整備、拡張機能の自動更新の制御強化、そしてエンタープライズ向けの Copilot 管理機能の追加が柱となるリリース。AI 連携と「エディタの中で完結する開発体験」を一段進める内容になっている。

## 主な変更点

### 統合ブラウザ（Integrated Browser）
- アドレスバーから、設定済みの検索エンジンを使って **Web 検索を直接実行**できるようになった。
- プレビュー機能として、リモートマシン上でしかアクセスできないポート/サービスへ HTTP(S) プロキシ経由で**セキュアに接続**できる。
- エージェントが forwarded ポートを正しく扱えるよう、URL の自動リライトに対応。

### 言語モデル / AI
- Language Models エディタに **Install Model Providers** ボタンを追加。Marketplace の「モデルプロバイダを提供する拡張機能」に絞り込んだ Extensions ビューを開ける。
- Copilot のステータスダッシュボードで、追加バジェットの消費率（%）を表示し、超過課金を抑止できる。

### 拡張機能の自動更新制御
- `extensions.autoUpdate` 設定を `on` / `off` のシンプルな値に整理（旧オプションは自動移行）。
- 新設定 `extensions.autoUpdateDelay`（単位: 時間、デフォルト 2 時間）で、更新インストールまでの遅延を設定可能。
- 自動更新の対象は有効な拡張機能のみ。無効化中の拡張は再有効化まで更新を待つ。

### エンタープライズ / Copilot 管理
- Windows・macOS のネイティブなデバイス管理（MDM）チャネル経由で、**管理された GitHub Copilot 設定を配布**できるように。ユーザーごとのサインインなしでポリシーを強制できる。

### 技術的アップデート
- Language Server Protocol サポートが **3.18** に前進。対応するクライアント/サーバパッケージを v10.0.0 に更新。

## 今後の注目点

- 統合ブラウザのリモートセキュア接続はまだ preview 段階。リモート開発（Dev Containers / SSH）ワークフローでの安定化が次の焦点。
- Model Provider の Marketplace 流通が広がることで、ローカル/サードパーティ LLM を VS Code から直接扱う構成が一般化する見込み。
- MDM での Copilot 設定配布は、組織展開におけるガバナンス要件への対応として要ウォッチ。
