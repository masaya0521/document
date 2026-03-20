# Tech Updates — 2026-03-20

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | JDK | 26 GA リリース | 10個のJEPを含むメジャーリリース。HTTP/3クライアントAPI、AOTオブジェクトキャッシング、G1 GCスループット改善、Applet API削除など | [Oracle Blog](https://blogs.oracle.com/java/the-arrival-of-java-26) |
| 2 | Vite | 8.0 リリース | Rust製統一バンドラー Rolldown を正式採用。ビルド速度10-30倍高速化、Devtools統合、Wasm SSR対応など | [Vite Blog](https://vite.dev/blog/announcing-vite8) |
| 3 | VS Code | 1.112 リリース | 統合ブラウザデバッグ、MCP サーバーサンドボックス化、エージェントの画像対応、モノレポカスタマイズ | [VS Code Updates](https://code.visualstudio.com/updates/v1_112) |
| 4 | Rust | 1.94.0 リリース | `array_windows` メソッド追加、AVX-512 FP16/AArch64 NEON FP16 の安定化、Cargo TOML v1.1 対応 | [Rust Blog](https://blog.rust-lang.org/2026/03/05/Rust-1.94.0/) |
| 5 | .NET | March 2026 サービスリリース | .NET 10.0.4 / 9.0.14 / 8.0.25 リリース。CVE-2026-26127（DoS脆弱性）など2件のセキュリティ修正 | [.NET Blog](https://devblogs.microsoft.com/dotnet/dotnet-and-dotnet-framework-march-2026-servicing-updates/) |
| 6 | Visual Studio | 2026 v18.3 更新 | JSON エディタのコアエディタ統合、JSON Schema $defs/$anchor 対応、コードエディタの左マージンスリム化 | [Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/releases/2026/release-notes) |
| 7 | WordPress | 7.0 RC1 延期 | リアルタイムコラボレーション・クライアントサイドメディア最適化の品質確保のため RC1 を3/24に延期。正式版は4/9予定 | [Make WordPress](https://make.wordpress.org/core/2026/03/19/wordpress-7-0-release-candidate-1-delayed/) |
| 8 | Tailwind CSS | Vite 8 対応 | Vite 8.0 リリース当日に `@tailwindcss/vite` の Vite 8 対応をマージ。peer dependency を `^8.0.0` に拡張 | [Benjamin Crozat](https://benjamincrozat.com/tailwind-css-vite-8-support) |
| 9 | C++26 | 最終承認投票へ | 3/23-28 ロンドン会議で最終承認投票。静的リフレクション、コントラクト、`std::execution`、SIMD型を含む | [Wikipedia](https://en.wikipedia.org/wiki/C++26) |
| 10 | Ruby | 3.2 EOL | Ruby 3.2 が2026年3月にEnd of Lifeを迎えた。セキュリティパッチの提供が終了 | [endoflife.date](https://endoflife.date/ruby) |

## Deep Dive

- [JDK 26 GA — 10個のJEPで進化するJava](./tu-jdk-26.md)
- [Vite 8.0 — Rolldown統合による統一バンドラー時代](./tu-vite-8.md)
