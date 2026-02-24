# Tech Updates — 2026-02-25

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 Beta リリース | JavaScript ベース最後のリリース。strict がデフォルト有効化、ES5 ターゲット・AMD/UMD を非推奨化。Go ベースの TypeScript 7 への移行準備 | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/) |
| 2 | Go | 1.26 リリース | 新パッケージ crypto/hpke（HPKE, RFC 9180）、実験的 SIMD サポート（archsimd）、runtime/secret パッケージ、GC 高速化 | [公式ブログ](https://go.dev/blog/go1.26) |
| 3 | PostgreSQL | 18.2, 17.8 等 + 臨時リリース予定 | 2/12 に全サポートバージョンの定期リリース。substring() の非 ASCII テキスト問題等のリグレッション発見により 2/26 に臨時リリース予定 | [公式](https://www.postgresql.org/about/news/out-of-cycle-release-scheduled-for-february-26-2026-3241/) |
| 4 | Django | 6.0.2 セキュリティリリース | 高深刻度の SQL インジェクション脆弱性 3 件を含む計 6 件のセキュリティ修正。FilteredRelation の制御文字経由の SQL インジェクション等 | [公式](https://www.djangoproject.com/weblog/2026/feb/03/security-releases/) |
| 5 | VS Code | 1.109（January 2026） | マルチエージェント開発プラットフォームへ進化。Claude Agent サポート（Public Preview）、エージェントセッション管理、プロンプトキューイング | [リリースノート](https://code.visualstudio.com/updates/v1_109) |
| 6 | Svelte | 5.47〜5.49 | `<select>` 要素の CSS カスタマイズ対応（5.47）、CSS パーサーを svelte/compiler から export（5.48）、ShadowRootInit サポート（5.49） | [公式ブログ](https://svelte.dev/blog/whats-new-in-svelte-february-2026) |
| 7 | Solidity | 0.8.34 リリース | IR パイプラインでの storage/transient storage クリアに関する高深刻度バグの修正。0.8.28〜0.8.33 が影響対象 | [公式](https://www.soliditylang.org/blog/2026/02/18/solidity-0.8.34-release-announcement/) |
| 8 | Rust | 1.93.1 パッチリリース | rustfmt に影響する ICE（Internal Compiler Error）の修正を含むパッチリリース | [公式ブログ](https://blog.rust-lang.org/2026/02/12/Rust-1.93.1/) |
| 9 | Nuxt | 4.3 リリース | Route Rule Layouts、ISR Payload Extraction、ドラッグ可能なエラーオーバーレイ、SSR スタイル最適化等のパフォーマンス改善 | [公式ブログ](https://nuxt.com/blog/v4-3) |
| 10 | WordPress | 6.9.1 リリース | 49 件のバグ修正。WordPress Studio v1.7.0 の CLI ツール大幅強化 | [公式](https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/) |

## Deep Dive

- [TypeScript 6.0 Beta — JavaScript ベース最後のリリースと Go 移行への道](./tu-typescript-6-beta.md)
- [Go 1.26 — ポスト量子暗号・SIMD サポートと言語改善](./tu-go-1-26.md)
