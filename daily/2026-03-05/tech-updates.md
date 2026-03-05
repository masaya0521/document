# Tech Updates — 2026-03-05

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Rust | v1.94.0 リリース | Unicode 17 対応、`array_windows` 等の標準ライブラリ安定化、Cargo config include キーの安定化 | [GitHub](https://releases.rs/docs/1.94.0/) |
| 2 | TypeScript | 6.0 Beta リリース | Go ベース TypeScript 7.0 への移行準備となる最後の JS ベースリリース。開発者に移行準備を促す | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-beta/) |
| 3 | Deno | v2.7.0 リリース | Temporal API の安定化、`deno create` コマンド追加、npm パッケージのスタンドアロン実行ファイルコンパイル対応 | [公式ブログ](https://deno.com/blog/v2.7) |
| 4 | Go | v1.26 リリース | `new` 関数の式オペランド対応、`go fix` 書き直し、crypto/hpke パッケージ追加、実験的 SIMD サポート | [公式ブログ](https://go.dev/blog/go1.26) |
| 5 | Tailwind CSS | v4.2.0 リリース | webpack プラグイン追加、mauve/olive/mist/taupe の 4 カラーパレット追加、論理プロパティユーティリティ | [GitHub](https://github.com/tailwindlabs/tailwindcss/releases) |
| 6 | VS Code | v1.110 (February 2026) | AI エージェントのネイティブブラウザアクセス、Claude の MCP サーバー対応、チャットの /fork コマンド | [公式](https://code.visualstudio.com/updates/v1_110) |
| 7 | pnpm | v10.29 / v10.30 | v10.30 で `pnpm why` をリバース依存ツリー表示に刷新、v10.29 で catalog: プロトコルの dlx 対応 | [GitHub](https://github.com/pnpm/pnpm/releases) |
| 8 | Django | 6.0.2 セキュリティリリース | SQL インジェクション脆弱性と HTML パース DoS 攻撃への対応。5.2.11、4.2.28 も同時リリース | [公式](https://www.djangoproject.com/weblog/2026/feb/03/security-releases/) |
| 9 | IntelliJ IDEA | 2026.1 EAP | ネイティブ Wayland サポート、スレッディングモデルの変更、EAP 3 まで公開中 | [JetBrains](https://youtrack.jetbrains.com/articles/IDEA-A-2100662608/IntelliJ-IDEA-2026.1-Latest-Builds) |
| 10 | Python | 3.14.3 リリース | 299 件のバグ修正・ビルド改善・ドキュメント変更を含むメンテナンスリリース | [公式](https://www.python.org/downloads/release/python-3143/) |

## Deep Dive

- [TypeScript 6.0 Beta — Go ベース TypeScript 7.0 への架け橋](./tu-typescript-6-beta.md)
- [Deno 2.7 — Temporal API 安定化とスタンドアロンコンパイル](./tu-deno-2-7.md)
