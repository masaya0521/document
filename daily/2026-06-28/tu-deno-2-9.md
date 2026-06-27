# Deno 2.9 — deno desktop とエコシステム移行の強化

- **日付**: 2026-06-28
- **カテゴリ**: Backend / Runtime
- **ソース**: [Deno 2.9 (Deno Blog)](https://deno.com/blog/v2.9), [Deno Releases (GitHub)](https://github.com/denoland/deno/releases)

## 概要

2026年6月25日、Deno 2.9 がリリースされた。最大の目玉は `deno desktop` で、Electron のようなボイラープレートなしに Web 技術（HTML/CSS/JavaScript）でネイティブデスクトップアプリを開発し、単一バイナリとして配布できるようになった。ランタイムにデスクトップ API を直接組み込むという方向性は、Deno を「サーバーサイドランタイム」から「アプリケーション配布プラットフォーム」へと拡張するものだ。

加えて、npm/pnpm/yarn/Bun の各種ロックファイルからの移行サポート、CSS モジュールインポート、テスト機能の大幅強化、`deno compile --bundle` のサイズ最適化、Node.js 26 互換など、既存エコシステムとの相互運用性を高めるアップデートが揃っている。

## 主な変更点

### deno desktop

- Web スタックでネイティブデスクトップアプリを構築し、単一バイナリで配布可能
- フレームワーク自動検出により、Next.js や Astro などの既存プロジェクトもそのままデスクトップ化できる
- `Deno.BrowserWindow`、`Deno.Tray` などのネイティブデスクトップ API がランタイムに組み込まれている

### npm 系ツールからの移行

```sh
deno install
```

- `package-lock.json` / `pnpm-lock.yaml` / `yarn.lock` / `bun.lock` から直接読み込み可能に
- 解決済みの正確なバージョンと integrity hash を保持したまま移行できる
- pnpm のワークスペース設定も自動マイグレーション。Node 互換レイヤーにより既存ツールも継続動作

### CSS モジュールインポート

```ts
import sheet from "./styles.css" with { type: "css" };
```

Web 標準の構文に沿って CSS をコンポーネント化でき、バンドラー不要でブラウザ・Deno の両方で実行できる。

### テスト機能の強化

- **スナップショット**: `t.assertSnapshot()` でビジュアルレグレッション検出
- **パラメータ化テスト**: `Deno.test.each()` でケースごとに独立してフィルタ可能なテストを登録
- その他、変更検知による選別実行、リトライ・リピート、カバレッジ閾値設定を追加

### deno compile --bundle

`--bundle` フラグで `node_modules` をバンドリング前処理し、大幅に軽量化（lodash の例で 11.6MB → 1.5MB）。単一マシンから全ターゲット向けバイナリを生成するクロスプラットフォーム対応も強化。

### Node.js 26 互換性

- 報告バージョンを 26 に更新
- `node:test` に `mock.module()` / `mock.timers` を追加
- ベアな Node 組み込みモジュール（`fs`、`path` など）を無条件に `node:fs` / `node:path` へマップ

## 破壊的変更・移行ガイド

メジャーバージョン据え置き（2.x 系）のため大きな破壊的変更はないが、Node 組み込みモジュールの解決挙動が変わっている点に注意。ベアな `fs` / `path` 等のインポートが常に `node:` プレフィックス付きへマップされるため、同名のローカルモジュールやサードパーティ依存と衝突する場合は import 指定の見直しが必要。

## 今後の注目点

- `deno desktop` が Electron / Tauri に対する現実的な選択肢として定着するか。バンドルサイズ・起動性能・OS 統合度の実測評価が鍵
- 各種ロックファイル移行サポートにより、Node/Bun プロジェクトの Deno への乗り換えハードルがどこまで下がるか
- CSS モジュールインポートなど Web 標準準拠の機能が、フロントエンドツールチェーンの簡素化にどう寄与するか
