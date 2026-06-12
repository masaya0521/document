# Python — 3.15.0 Beta 2 リリース（feature freeze 確定）

- **日付**: 2026-06-12（Beta 2 リリースは 2026-06-02）
- **カテゴリ**: Language
- **ソース**: [python.org 3.15.0b2](https://www.python.org/downloads/release/python-3150b2/), [PEP 790 — Python 3.15 Release Schedule](https://peps.python.org/pep-0790/)

## 概要

Python 3.15.0 の Beta 2 が 6 月 2 日にリリースされた。5 月 7 日の Beta 1 で feature freeze に入っており、ここから 10 月 1 日の最終リリースまではバグ修正と仕上げのみが行われる。3.15 は「起動の高速化（lazy imports）」「JIT の本格的な性能向上」「フリースレッド CPython の安定 ABI」という、ここ数年の CPython 高速化・並列化路線が形になるリリース。

## 主な変更点

### 言語・標準ライブラリ

- **PEP 810 — 明示的 lazy imports**: `lazy import` 構文でインポートを使用時まで遅延し、起動時間を短縮。CLI ツールや大規模アプリの起動高速化に直結する
- **PEP 814 — `frozendict` 組み込み型**: 不変マッピングが標準で利用可能に
- **PEP 661 — `sentinel` 組み込み**: センチネル値の標準的な定義方法を提供
- **PEP 798 — 内包表記でのアンパッキング**: `[*x for x in xs]` のような記法が可能に
- **PEP 686 — UTF-8 モードがデフォルトに**: ロケール依存のテキストエンコーディングが原則 UTF-8 に統一される
- **PEP 728 — TypedDict の extra items**、**PEP 747 — TypeForm**、**PEP 800** など型システムの拡張

### パフォーマンス・ランタイム

- **JIT コンパイラの改善**: インタプリタ比で x86-64 Linux で平均 8〜9%、Apple silicon macOS で 12〜13% の性能向上（一部コードは最大 15% 低下のケースもあり）
- **PEP 799 / Tachyon — ゼロオーバーヘッドのサンプリングプロファイラ**: 本番環境でのプロファイリングが現実的に
- **PEP 803 / 820 / 793 — フリースレッド CPython の安定 ABI**: free-threaded ビルド向け拡張モジュールの配布が容易になる
- **PEP 831 — フレームポインタのデフォルト有効化**: perf 等のシステムレベルツールからの可視性向上
- Windows 64bit バイナリがテールコーリングインタプリタを採用

## 破壊的変更・移行ガイド

- **UTF-8 デフォルト化（PEP 686）** が実質的に最大の互換性リスク。Windows 環境や非 UTF-8 ロケールで `open()` のエンコーディング未指定に依存しているコードは挙動が変わる。`encoding="utf-8"` の明示、または `EncodingWarning` を有効にした事前検証が推奨
- lazy imports は明示的なオプトイン構文のため既存コードへの影響はない

## 今後の注目点

- Beta 3（6/23）、Beta 4（7/18）を経て **2026-10-01 に 3.15.0 GA** 予定
- JIT が「一部コードで遅くなる」問題の解消度合い
- フリースレッドビルドの安定 ABI を受けた、主要ライブラリ（NumPy 等）の free-threaded wheel 配布の広がり
- lazy imports のエコシステム側の採用（CLI フレームワーク、大規模 Web アプリの起動時間改善事例）
