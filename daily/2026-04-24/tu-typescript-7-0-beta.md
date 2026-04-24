# TypeScript 7.0 Beta — Go 実装コンパイラで 10x 高速化

- **日付**: 2026-04-21
- **カテゴリ**: Language / Dev Tool
- **ソース**: [Announcing TypeScript 7.0 Beta — Microsoft DevBlogs](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0-beta/), [TypeScript 7.0 Beta Arrives on Go-Based Foundation With 10x Speed Claim — Visual Studio Magazine](https://visualstudiomagazine.com/articles/2026/04/21/typescript-7-0-beta-arrives-on-go-based-foundation-with-10x-speed-claim.aspx)

## 概要

Microsoft は 2026-04-21 に TypeScript 7.0 Beta をリリースしました。これまでブートストラップされた JavaScript 実装だったコンパイラを Go に書き直し（コードネーム "Project Corsa"）、ネイティブコード速度と共有メモリ並列処理により TypeScript 6.0 比で約 10 倍高速化したと発表されています。これは TypeScript の誕生以来最大のアーキテクチャ変更であり、型チェッカーのセマンティクスは 6.0 と構造的に同一を維持しつつ、「速い TypeScript」という長年の課題に決着をつけるマイルストーンです。

Bloomberg、Canva、Figma、Google、Lattice、Linear、Miro、Notion、Slack、Vanta、Vercel、VoidZero といった大規模な社内 / 外部ユーザーによる試験運用を経ており、ベータの安定度はそれなりに高い状態で公開されています。

## 主な変更点

### Go 実装コンパイラ `tsgo`

- インストールは npm 経由で `npm i -D @typescript/native-preview@beta`。実行コマンドは従来の `tsc` ではなく `tsgo` に置き換わる
- VS Code 拡張も公開されており、エディタでも同等の高速化が得られる
- 型チェックロジックは既存実装からメソッド的に移植され、6.0 と構造的に同じセマンティクスで動作する（書き直しではなく移植）

### 並列化オプション

- `--checkers`（デフォルト 4）: 型チェックを並列実行するスレッド数
- `--builders`: project references ビルドの並列度
- `--singleThreaded`: デバッグやリソース制限環境向けにシングルスレッドで動かす

### 既存プロジェクトとの共存

- ベータは独立したパッケージ名 / エントリーポイント（`tsgo`）として提供され、従来の `tsc` と衝突しない
- 互換性パッケージ `@typescript/typescript6` を使うと、同一リポジトリ内で両バージョンを併用可能
- 段階的な検証・移行を前提とした設計

## 破壊的変更・移行ガイド

7.0 では歴史的な互換性負債が整理され、デフォルトが「現代的」な値に寄せられます。

- `strict: true` がデフォルト（6.0 では `false`）
- `module` のデフォルトが `esnext`
- 以下のレガシーオプションはサポートされなくなる
  - `es5` ターゲット
  - `amd` / `umd` モジュール形式
  - `baseUrl`（明示的に設定する場合を除き使用不可）
- `rootDir` / `types` の設定は明示的な指定が必要になるケースがある

既存プロジェクトを 7.0 へ段階的に移行するなら、次の流れが安全です。

1. `@typescript/native-preview@beta` を dev dependency に追加
2. `tsc` との差分を `tsgo` で並行検証（`--checkers 1` で挙動を安定させる）
3. `strict: true` 相当の型エラーを洗い出す
4. CI での型チェックを `tsgo` に切り替え、`tsc` はフォールバックとして `@typescript/typescript6` を利用
5. 問題がなければ通常の TypeScript 7.0 リリース後に `tsc` → `tsgo` に完全移行

## 今後の注目点

- **安定版のスケジュール**: 2 ヶ月以内の GA を目標とし、数週間前に RC を予定。2026 年 6 月末〜7 月上旬が有力
- **エコシステム対応**: ts-loader / ts-jest / Next.js / Remix / Vite plugin など、周辺ツールが `tsgo` バイナリを呼び出せるよう対応待ち
- **型チェッカーのプラガビリティ**: Go 実装になったことで、今後 WASM 配布や他ホスト言語への埋め込みが現実的になる
- **監視ポイント**: モノレポでの実測値（`tsc --noEmit` 比）、IDE の補完体感、`skipLibCheck` 無しでの挙動、型推論の差分ケース
