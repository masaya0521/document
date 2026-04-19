# Node.js 24.15.0 LTS — Explicit Resource Management と ClangCL 必須化

- **日付**: 2026-04-20（リリース日: 2026-04-15）
- **カテゴリ**: Backend / Runtime
- **ソース**: [versionlog Node.js 24](https://versionlog.com/nodejs/24/), [CHANGELOG_V24.md](https://github.com/nodejs/node/blob/main/doc/changelogs/CHANGELOG_V24.md), [LogRocket: Node.js 24](https://blog.logrocket.com/node-js-24-new/)

## 概要

Node.js 24.15.0 LTS は 24 系の最新メンテナンスリリースであり、LTS フェーズ継続中のリリースラインに対するパッチ更新。24 系は 2024-10 に GA、2025 から LTS 化し、本バージョンのサポート期限は 2028-04-30 まで。

メジャーバージョン 24 の大きな差分は 2025 年の GA 時点で入っており、4 月のリリースは 24 系の安定化を続ける位置付けだが、累積すると V8 13.6 + Undici 7 の新機能を本番で活用できる時期が来たことを意味する。とくに `using` / `await using` 宣言の正式サポートと、ビルドチェーンでの MSVC 廃止は、既存 24 系ユーザーがパッチレベルで踏む破壊的変更となりうる。

## 主な変更点

### Explicit Resource Management (V8 13.6)

TC39 の Explicit Resource Management プロポーザルがネイティブサポートされ、`using` / `await using` 宣言でスコープを抜けたときに `[Symbol.dispose]()` / `[Symbol.asyncDispose]()` を自動呼び出しできる。

```ts
async function copyStream(src: string, dst: string) {
  await using input = await fs.open(src, 'r');
  await using output = await fs.open(dst, 'w');
  await input.readableWebStream().pipeTo(output.writableWebStream());
  // ブロック終端で両ファイルが自動クローズ
}
```

同期版では `DisposableStack`、非同期版では `AsyncDisposableStack` によって複数リソースをまとめて破棄できる。try/finally を重ねる従来パターンと比べ、ネストが減りリーク耐性が上がる。

### Undici 7 (HTTP client)

- `fetch` の内部実装が Undici 7 に更新され、HTTP/2 サポートと spec 準拠が強化
- リクエスト/レスポンスのハンドリングで内部的な最適化が入り、高負荷時のスループットが向上
- ほとんどは内部変更だが、カスタム Agent を書いているコードには影響し得る

### MSVC サポートの廃止（破壊的変更）

Windows でのネイティブビルドは MSVC が非サポートとなり、`ClangCL`（Clang の MSVC 互換出力）が必須になった。Node.js 本体のビルド・ネイティブアドオンのビルドの両方に影響する。

## 破壊的変更・移行ガイド

- **Node.js 本体をソースビルドしている環境**: Visual Studio のワークロードに「C++ による Clang ツール」を追加し、`vcbuild.bat` 実行前に `set CC=clang-cl` / `set CXX=clang-cl` を設定する。
- **ネイティブアドオンを配布するパッケージ**: prebuilt バイナリの再ビルドが必要。`node-gyp` は MSVS_VERSION 自動判定で ClangCL を選ぶよう更新されている前提で動くため、CI の Windows runner で `node-gyp` のバージョンを最新化する。
- **`using` を使う前の確認**: TypeScript 側の対応は TS 5.2+ で target を ES2022 以降、lib に `ESNext.Disposable` を含める必要あり。ビルド tooling（esbuild/Vite/Rolldown など）の down-level transform も確認。

## 今後の注目点

- Node.js 26 (2025-10 予定) では TypeScript のネイティブサポート（type stripping）と Permission Model のさらなる改善が議論中
- Undici 7 のさらなる最適化で `fetch` 性能が底上げされる見込み
- V8 13.6 以降の新しい JS プロポーザル（Iterator Helpers Stage 4 など）の追随
