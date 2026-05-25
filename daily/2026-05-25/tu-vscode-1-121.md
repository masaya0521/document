# VS Code 1.121 — リモートエージェントと Agent Host Protocol

- **日付**: 2026-05-20
- **カテゴリ**: Dev Tool
- **ソース**: [VS Code 1.121 リリースノート](https://code.visualstudio.com/updates/v1_121), [Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/05/20/vs-code-1-121-adds-remote-agents-built-in-html-and-mermaid-previews.aspx)

## 概要

VS Code 1.121 は、AI エージェントの活用範囲を大幅に拡張するリリース。SSH や Dev Tunnels を経由してリモートマシン上でエージェントセッションを実行できる「Remote Agent Sessions」が Preview として導入され、クライアント切断後もリモート側で作業が継続する。また、この機能を支える新しいオープンプロトコル「Agent Host Protocol (AHP)」の策定が進行中。

## 主な変更点

### Remote Agent Sessions (Preview)

- Agents ウィンドウから SSH または Dev Tunnels 経由でリモートマシン上のエージェントセッションを起動
- リモートエージェントホストは長時間実行プロセスとして動作し、**クライアント切断後もセッションが継続**
- ラップトップを閉じてもリモート側で作業が進行し、再接続時に結果を確認可能
- 複数クライアントから同一エージェントホストへの接続をサポート

### Agent Host Protocol (AHP)

- エージェントセッションの管理を標準化する新しいオープンプロトコル
- VS Code CLI のエージェントホストに任意のクライアントから接続可能
- 公開仕様として独立して開発中。IDE 間の相互運用を見据えた設計

### Mermaid プレビュー (組み込み)

- Matt Bierner 氏の拡張機能「Markdown Preview Mermaid Support」がコアに統合され、新しい組み込み拡張機能「Mermaid Markdown Features」に
- マークダウンプレビュー、ノートブックセル、チャット内で Mermaid ダイアグラムを直接レンダリング
- パン・ズーム機能で大きなダイアグラムの閲覧が容易
- 右クリックで Mermaid ソースコードのコピーが可能

### HTML プレビュー (組み込み)

- 拡張機能不要でローカル HTML ファイルを統合ブラウザでプレビュー
- ファイルエクスプローラーの右クリック、またはエディタタイトルバーのプレビューアイコンから起動

### AI・エージェント関連

- **ユーティリティモデル設定**: `chat.utilityModel` / `chat.utilitySmallModel` で軽量タスク用のモデルをカスタマイズ
- **Claude Agent 自動許可モード**: 安全性チェック付きで権限プロンプトを削減
- **ターミナル出力圧縮**: pytest、jest、tsc などのテストランナー出力をエージェント向けに自動圧縮
- **バックグラウンドターミナル管理**: エージェントが作成したバックグラウンドターミナルの自動クリーンアップ

## 今後の注目点

- AHP の仕様策定の進捗と他 IDE での採用状況
- Remote Agent Sessions の GA（正式版）リリース時期
- リモートエージェントとローカルエージェントの使い分けパターンの確立
- Mermaid 対応の拡張（追加ダイアグラムタイプ、ライブ編集連動等）
