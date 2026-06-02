# Bun v1.3.14 — Bun.Image と HTTP/3 対応

- **日付**: 2026-06-02（v1.3.14 は 2026-05-14 リリース）
- **カテゴリ**: Backend（ランタイム / ツールチェーン）
- **ソース**: [Bun v1.3.14 Blog](https://bun.com/blog/bun-v1.3.14), [Bun Releases](https://github.com/oven-sh/bun/releases)

## 概要

Bun v1.3.14 が 2026年5月14日にリリースされた（92 件のバグ修正を含む）。注目は **組み込み画像処理 API `Bun.Image`** と、**fetch / `Bun.serve()` の HTTP/2・HTTP/3(QUIC) 対応**。`Bun.Image` はネイティブモジュール不要で Sharp の代替を狙うもので、メタデータ取得で最大70倍、画像変換で 1.2〜1.38 倍の高速化を謳う。さらに isolated linker のグローバルストアにより warm install が 7倍高速化するなど、ランタイム・パッケージマネージャ・テストランナーを一体で提供する Bun の強みがさらに強化された。

## 主な変更点

### Bun.Image — 組み込み画像処理 API

ネイティブ依存なしで画像のデコード・変換・エンコードが可能。Node.js の Sharp のドロップイン代替を意図している。

```javascript
// リサイズ・回転して WebP に変換
await Bun.file("photo.jpg")
  .image()
  .resize(1024, 1024, { fit: "inside" })
  .rotate(90)
  .webp({ quality: 85 })
  .write("thumb.webp");
```

対応形式は JPEG / PNG / WebP / GIF / BMP（全プラットフォーム）に加え、HEIC・AVIF・TIFF（macOS / Windows）。

### HTTP/2・HTTP/3 対応

fetch での HTTP/2 クライアント（TLS ALPN で `h2` をネゴシエート、同一オリジンへの並行リクエストを1接続で多重化）と、`Bun.serve()` での HTTP/3(QUIC) サーバーが実験的に追加された。

```javascript
// HTTP/3 (QUIC) サーバー
Bun.serve({
  port: 443,
  tls: { cert, key },
  http3: true,
  fetch(req) {
    return new Response("served over h3");
  },
});
```

ベンチマークでは HTTP/3 が HTTPS/1.1 比で約50%高速とされる。

### Isolated Linker のグローバルストア

パッケージをグローバルな `<cache>/links/` に一度だけ実体化し、各プロジェクトの `node_modules` はシンボリックリンク経由で参照する。これにより warm install が 7倍高速化。

```toml
# bunfig.toml
[install]
globalStore = true
```

### その他の主要機能

- **`fs.watch()` の再実装**: Linux / macOS で再帰監視を改善。削除後に再作成されたファイルの追跡にも対応。
- **`--no-orphans` フラグ**: 親プロセス終了時に子プロセスを強制終了。
- **`process.execve()` 実装**: Node.js v24 互換のプロセス置き換え。
- **Bun.Terminal（Windows ConPTY 対応）**: Windows でターミナル機能が動作。
- **FreeBSD / Android 公式ビルド**の提供開始。
- **SSL_CTX キャッシング**: TLS 接続の設定重複を排除しメモリ削減。

## 破壊的変更・移行ガイド

メンテナンスリリースのため大きな破壊的変更はないが、新機能の多くは実験的（HTTP/3 など）。本番採用時は段階的に検証すること。`globalStore` はオプトインのため、既存プロジェクトの挙動はデフォルトでは変わらない。

## 今後の注目点

- `Bun.Image` が Sharp を実運用で代替できるか（対応フォーマット・カラープロファイル・パフォーマンスの実測）。
- HTTP/3(QUIC) サーバーの安定化と本番運用実績。
- Anthropic 傘下となった Bun が Claude Code のランタイムとして使われている文脈もあり、ツールチェーン全体の進化ペースは引き続き速い。
