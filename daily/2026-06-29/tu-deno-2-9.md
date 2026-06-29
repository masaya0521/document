# Deno — v2.9（deno desktop とパッケージマネージャ移行）

- **日付**: 2026-06-29
- **カテゴリ**: Backend / Build Tool（JavaScript / TypeScript ランタイム）
- **ソース**: [Deno Blog（Product Update）](https://deno.com/blog?tag=product-update), [Deno endoflife.date](https://endoflife.date/deno)

## 概要

2026 年 6 月 25 日、Deno チームは Deno 2.9 を公開した。今回のリリースは「ランタイム + ツールチェーン」としての Deno をさらにアプリケーション開発プラットフォームへ押し上げる内容で、目玉は Web 技術からネイティブデスクトップアプリを生成する `deno desktop` の導入である。あわせて、npm / pnpm / yarn / Bun といった既存エコシステムからの移行を「ファーストクラス」でサポートし、Node.js 26 互換を確保することで、Node 中心のプロジェクトでも Deno への乗り換え障壁を大きく下げている。

Bun 1.3 が「単一バイナリで全部入り」を志向するのに対し、Deno 2.9 は「標準準拠（Web API・CSS modules）」と「成果物の配布（desktop / compile）」の両面を強化しており、両者の競争軸の違いが鮮明になってきた。

## 主な変更点

- **`deno desktop`**: HTML / CSS / TypeScript といった Web 技術でネイティブデスクトップアプリを構築。Electron 的なワークフローを Deno の標準ツールで完結できる。
- **パッケージマネージャからのファーストクラス移行**: npm / pnpm / yarn / Bun のプロジェクトを Deno へ移行する導線を公式サポート。lockfile や依存解決の互換性を取り込む。
- **CSS module imports**: CSS を JavaScript / TypeScript モジュールとして直接 import 可能に。バンドラなしでのスタイル管理が容易になる。
- **テスト機能の強化**: スナップショットテストとパラメータ化テスト（parameterized testing）に対応。
- **`deno compile --bundle` のバイナリ縮小**: 単一実行ファイルへのコンパイル時の成果物サイズを削減。
- **Node.js 26 互換**: 最新の Node.js API サーフェスとの互換性を確保し、Node 資産の再利用性を向上。

## 破壊的変更・移行ガイド

- 公式ブログ要約の範囲では大きな破壊的変更は強調されていないが、Node.js 26 互換レイヤやパッケージマネージャ移行まわりは挙動が変わる可能性があるため、既存プロジェクトでは CI 上で `deno test` / `deno check` を通して回帰を確認することを推奨。
- `deno desktop` は新規追加機能のため、既存コードへの影響はなし。デスクトップ配布を検討するプロジェクトでの新規採用が中心となる。

## 今後の注目点

- `deno desktop` が Tauri / Electron のシェアにどこまで食い込むか。Web 標準志向の DX とバイナリサイズが評価軸になる。
- npm/pnpm/yarn/Bun 移行サポートの完成度が、Node エコシステムからの実移行を加速させるか。
- Bun（Anthropic 傘下で Claude Code のランタイム）との「全部入りランタイム」競争の行方。
