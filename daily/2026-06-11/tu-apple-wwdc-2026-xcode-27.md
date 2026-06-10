# Apple WWDC 2026 — Xcode 27 と Intelligence フレームワーク

- **日付**: 2026-06-11（WWDC 2026 は 6/8〜6/12 開催）
- **カテゴリ**: Dev Tool / Frontend（モバイル・デスクトップ）
- **ソース**: [Apple Newsroom](https://www.apple.com/newsroom/2026/06/apple-aids-app-development-with-new-intelligence-frameworks-and-advanced-tools/), [MacRumors](https://www.macrumors.com/2026/06/09/apple-outlines-major-ai-and-developer-tool-updates/)

## 概要

Apple は WWDC 2026 の Platforms State of the Union で、開発者向けのインテリジェンスフレームワークと開発ツールの大規模なアップデートを発表した。中核となるのは新しい **Xcode 27** と、オンデバイス／クラウドの AI モデルをネイティブの Swift API から扱える **Foundation Models フレームワーク** の拡張である。Xcode はサードパーティのコーディングエージェント（Anthropic・Google・OpenAI）を統合し、Model Context Protocol（MCP）にも対応することで、エージェント駆動の開発体験を IDE に取り込んだ。

AI を「アプリに組み込む側」と「開発に使う側」の両面で強化している点が今回の特徴で、Apple プラットフォーム向けアプリ開発のワークフローが大きく変わる可能性がある。

## 主な変更点

### Xcode 27

- **エージェントコーディング**: Anthropic・Google・OpenAI のモデル／エージェントを統合。インタラクティブなプランニング、マルチターン Q&A、Markdown をレンダリングできる canvas を搭載
- **Model Context Protocol（MCP）対応**: GitHub・Figma などの外部ツールとシームレスに連携
- **Device Hub**: 物理デバイス管理を刷新し、シミュレータからの移行先に。シミュレータサイズの動的変更に対応
- **パフォーマンス**: Apple silicon 専用化によりサイズを 30% 削減。Xcode Cloud は最大 2 倍高速化

### Intelligence フレームワーク

- **Foundation Models フレームワーク**: 単一のネイティブ Swift API で、より強力なオンデバイスモデルと **画像入力** をサポート。同じ API から Claude や Gemini などサードパーティのサーバーサイドモデルを呼び出せるように
- **Core AI フレームワーク**: カスタムのオンデバイスモデルを実行する新フレームワーク。事前（AoT）コンパイル、専用 Instruments、PyTorch モデルを Apple silicon 向けに変換する Python ツールを提供。Siri の基盤にも採用
- **Dynamic Profiles**: マルチエージェントワークフローを構築するための、モデル動作をリアルタイム更新できる仕組み
- **無料クラウドアクセス**: 累計初回ダウンロードが 200 万未満の開発者向けに、Private Cloud Compute 上の Apple Foundation Models を無料提供

### UI・その他

- **SwiftUI**: 効率的なステート初期化、再利用可能なコンテナを追加
- **Swift 6.4**: 警告抑制、コンパイラ診断の改善
- **Spatial Preview フレームワーク**: Mac アプリが Apple Vision Pro 装着者の周囲空間に 3D モデルをリアルタイムで展開可能に

## 破壊的変更・移行ガイド

- Xcode 27 は **Apple silicon 専用** となり、Intel Mac はサポート対象外。Intel 機での開発を継続する場合は旧バージョンの維持が必要
- Foundation Models の API は画像入力・サーバーサイドモデル対応で拡張されており、既存実装はそのまま動作するが、新機能を使う場合は SDK 更新が前提

## 今後の注目点

- サードパーティエージェント（Claude・Gemini・GPT）の Xcode 統合が、実際の開発生産性にどの程度寄与するか
- Foundation Models のサーバーサイドモデル呼び出しが、オンデバイス中心だった Apple の AI 戦略にどう影響するか
- MCP 対応により、Apple エコシステム外のツール連携がどこまで広がるか
