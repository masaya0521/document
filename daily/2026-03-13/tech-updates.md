# Tech Updates — 2026-03-13

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | 6.0 RC | JS ベース最終リリース。Go ベース 7.0 への橋渡し版。RegExp.escape、subpath imports、import assertions の非推奨化 | [TypeScript Blog](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0-rc/) |
| 2 | VS Code | 1.111（週次リリース開始） | 週次リリースへの移行。AI エージェントの Autopilot モード、エージェントスコープフック、デバッグイベントスナップショット | [VS Code Updates](https://code.visualstudio.com/updates/v1_111) |
| 3 | Rust | 1.94.0 | array_windows によるスライス反復、AVX-512 FP16 / AArch64 NEON FP16 intrinsics 安定化、Cargo の TOML 1.1 サポート | [Phoronix](https://www.phoronix.com/news/Rust-1.94-Released) |
| 4 | Go | 1.26 | Green Tea GC デフォルト化、cgo オーバーヘッド 30% 削減、go fix 刷新、crypto/hpke 追加、実験的 SIMD パッケージ | [Go Blog](https://go.dev/blog/go1.26) |
| 5 | Vue.js | 3.6.0-beta | Vapor Mode（仮想 DOM 不要のコンパイルモード）が機能完成。alien-signals ベースのリアクティビティ大幅改善 | [GitHub Release](https://github.com/vuejs/core/releases/tag/v3.6.0-beta.1) |
| 6 | PostgreSQL | 18.3 / 17.9 等 | スタンバイの transaction ステータスエラー修正、substring() のエンコーディングバグ修正、pg_trgm クラッシュ修正 | [PostgreSQL](https://www.postgresql.org/about/news/postgresql-183-179-1613-1517-and-1422-released-3246/) |
| 7 | Kubernetes | 1.33 パッチ / Ingress NGINX 廃止 | コンテナサイドカーのネイティブサポート安定化。2026年3月に Ingress NGINX が公式廃止 | [Kubernetes](https://kubernetes.io/releases/1.33/) |
| 8 | Python | 3.14.3 | テンプレート文字列リテラル（t-strings）、アノテーション遅延評価、Zstandard 圧縮モジュール追加、テールコールインタプリタ | [Python.org](https://www.python.org/downloads/release/python-3143/) |
| 9 | Svelte | CLI sv@0.12.0 / 月次アップデート | better-auth が公式アドオンに。programmatic Svelte の createContext、HTML タグ内コメント対応 | [Svelte Blog](https://svelte.dev/blog/whats-new-in-svelte-march-2026) |
| 10 | JetBrains | CLion 2026.1 EAP / ReSharper for VS Code | CLion 2026.1 EAP 終盤、IntelliJ 系 IDE の Wayland ネイティブ対応（2026.1〜）、ReSharper の VS Code 拡張リリース | [JetBrains Blog](https://blog.jetbrains.com/category/releases/) |

## Deep Dive

- [TypeScript 6.0 RC — Go ベースの未来への架け橋](./tu-typescript-6-0-rc.md)
- [VS Code 1.111 — 週次リリースと Autopilot モード](./tu-vscode-1-111-autopilot.md)
