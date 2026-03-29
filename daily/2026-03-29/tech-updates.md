# Tech Updates — 2026-03-29

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | TypeScript | v6.0 リリース | JavaScript ベースの最終リリース。`strict: true` デフォルト化、`target: es5` 廃止など大量の非推奨化。Go ネイティブの 7.0 への橋渡し | [公式ブログ](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/) |
| 2 | Vite | v8.0 リリース | Rolldown（Rust 製統一バンドラー）を採用。esbuild + Rollup の二重構成を解消し、ビルド速度 10-30x 向上 | [公式ブログ](https://vite.dev/blog/announcing-vite8) |
| 3 | C++26 | WG21 最終承認 | 3/28 ロンドン会議で C++26 ドラフト最終承認。コンパイル時リフレクション、コントラクト、Sender/Receiver 型を含む | [Wikipedia](https://en.wikipedia.org/wiki/C++26) |
| 4 | VS Code | v1.111（週次リリース開始） | 週次 Stable リリースに移行。Autopilot（プレビュー）、エージェント権限制御、エージェントフックなどの AI エージェント機能を大幅強化 | [リリースノート](https://code.visualstudio.com/updates/v1_111) |
| 5 | Angular | v21.2.5 | Zoneless Change Detection がデフォルト化、Vitest がデフォルトテストランナーに、Signal Forms 導入 | [Angular](https://angular.dev/events/v21) |
| 6 | JetBrains IDE | 2026.1 一斉リリース | IntelliJ IDEA / WebStorm / PhpStorm / CLion が同時リリース。ACP 経由の外部 AI エージェント統合、Git worktree サポート | [IntelliJ](https://blog.jetbrains.com/idea/2026/03/intellij-idea-2026-1/) |
| 7 | Tailwind CSS | v4.2.2 | webpack プラグイン追加、新カラー 4 色（mauve / olive / mist / taupe）、論理プロパティユーティリティの拡充 | [GitHub Releases](https://github.com/tailwindlabs/tailwindcss/releases) |
| 8 | Svelte | 2026年3月アップデート | `createContext` サポート、`{@html}` での TrustedHTML 対応、サーバーサイドエラーバウンダリ追加 | [公式ブログ](https://svelte.dev/blog/whats-new-in-svelte-march-2026) |
| 9 | ReSharper for VS Code | 正式リリース | 1年のパブリックプレビューを経て正式版に。C# コード解析を VS Code / Cursor / Google Antigravity で利用可能に | [JetBrains ブログ](https://blog.jetbrains.com/dotnet/2026/03/05/resharper-for-visual-studio-code-cursor-and-compatible-editors-is-out/) |
| 10 | @vitejs/plugin-react | v6（Vite 8 同梱） | Babel から Oxc（Rust 製コンパイラ）へ移行。JSX / デコレータ変換が高速化 | [Vite 8 ブログ](https://vite.dev/blog/announcing-vite8) |

## Deep Dive

- [TypeScript 6.0 — JavaScript ベース最終リリースと 7.0 への移行準備](./tu-typescript-6-0.md)
- [Vite 8.0 — Rolldown 統合による統一バンドラーアーキテクチャ](./tu-vite-8-0.md)
