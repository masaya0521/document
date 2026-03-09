# Deno 2.7 — Temporal API 安定化と Windows ARM サポート

- **日付**: 2026-03-05
- **カテゴリ**: Backend
- **ソース**: [Deno Blog](https://deno.com/blog/v2.7), [heise online](https://www.heise.de/en/news/Deno-2-7-sharpens-Node-js-compatibility-and-stabilizes-Temporal-11190888.html), [GitHub Release](https://github.com/denoland/deno/releases/tag/v2.7.2)

## 概要

Deno 2.7 は 2026年3月にリリースされ、長らく実験的だった Temporal API の安定化、Windows ARM の公式サポート、npm package.json の overrides フィールド対応など、実用性を大きく向上させるアップデートを含む。V8 エンジンも 14.5 にアップグレードされ、最新の JavaScript 機能とパフォーマンス改善が反映されている。

## 主な変更点

### Temporal API の安定化

Temporal API が実験的ステータスを脱し、`--unstable-temporal` フラグが不要になった。Chrome 144（2026年1月）で Temporal API がデフォルト有効になったことに合わせた対応。

Temporal は `Date` オブジェクトの長年の問題（タイムゾーン処理の不備、ミュータブルな設計等）を解決する新しい日時 API で、以下のような利点がある:

```typescript
// イミュータブルな日時操作
const now = Temporal.Now.plainDateTimeISO();
const nextWeek = now.add({ days: 7 });

// タイムゾーンを明示的に扱える
const tokyo = Temporal.Now.zonedDateTimeISO("Asia/Tokyo");
const newYork = tokyo.withTimeZone("America/New_York");

// 期間の正確な計算
const duration = now.until(nextWeek);
console.log(duration.days); // 7
```

### Windows ARM サポート

`aarch64-pc-windows-msvc` ターゲットの公式ビルドが初めて提供された。Surface Pro X や Snapdragon ベースのノートブック等で、エミュレーション層なしにネイティブ実行が可能になる。

### npm package.json overrides

`package.json` の `overrides` フィールドに対応し、依存関係ツリーの深い階層にあるパッケージのバージョンを制御できるようになった。セキュリティ脆弱性の修正や互換性の強制に有用。

```json
{
  "overrides": {
    "lodash": "4.17.21",
    "some-package": {
      "nested-dep": "2.0.0"
    }
  }
}
```

### Node.js 互換性の改善

- `node:worker_threads` の挙動改善
- `node:child_process` の互換性向上
- `node:zlib` の調整
- `node:sqlite` の改善
- `navigator.platform` API の追加
- Web Crypto API での SHA3 サポート
- `CompressionStream` / `DecompressionStream` での Brotli サポート

### V8 14.5 へのアップグレード

最新の V8 エンジンにより、パフォーマンス改善と新しい JavaScript 機能が利用可能に。

## 今後の注目点

- Deno 2.6 で導入された `tsgo`（Go ベースの TypeScript 型チェッカー）の成熟度向上に注目
- Deno 2.6 の `dx` コマンド（npx の代替）のエコシステムでの普及
- Node.js 互換性のさらなる向上により、既存の Node.js プロジェクトからの移行がより容易に
- Temporal API の安定化により、ブラウザとサーバーサイドで統一的な日時処理が可能に
