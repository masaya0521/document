# Tech Updates — 2026-04-15

| # | プロジェクト | バージョン / 内容 | 概要 | ソース |
|---|-------------|-------------------|------|--------|
| 1 | Kubernetes | v1.36 リリース予定 (4/22) | MutatingAdmissionPolicy が GA、gitRepo ボリューム完全削除、DRA 分割可能デバイス対応、Ingress NGINX 引退に伴う Gateway API 移行推奨 | [Sneak Peek](https://kubernetes.io/blog/2026/03/30/kubernetes-v1-36-sneak-peek/) |
| 2 | TypeScript | 7.0 Native Preview (dev.20260413.1) | Go ベース新コンパイラ tsgo の開発版。型チェックほぼ完全（残り74テスト）、既存比 7-10x 高速化、VS Code 拡張でエディタ機能も利用可能に | [npm](https://www.npmjs.com/package/@typescript/native-preview) |
| 3 | VS Code | 1.115 (4/8) | 新しい VS Code Agents コンパニオンアプリ、統合ブラウザ改善、バックグラウンドターミナル操作、Copilot Business/Enterprise 向け BYOK 対応 | [Release Notes](https://code.visualstudio.com/updates/v1_115) |
| 4 | Docker Engine | 29.4.0 (4/3) | AuthZ プラグインバイパス (CVE-2026-34040)、プラグインインストール時の権限昇格 (CVE-2026-33997) 等のセキュリティ修正。BuildKit v0.29.0、containerd v2.2.2 へ更新 | [Release Notes](https://docs.docker.com/engine/release-notes/29/) |
| 5 | Ruby | 3.4.3 (4/14) | RubyKaigi 直前のメンテナンスリリース。バグ修正とセキュリティ修正を含む安定版アップデート | [Release](https://www.ruby-lang.org/en/news/2025/04/14/ruby-3-4-3-released/) |
| 6 | PostgreSQL | 19 Feature Freeze (4/8) | PostgreSQL 19 のフィーチャーフリーズ開始。9月の正式リリースに向けて安定化フェーズへ移行 | [Announcement](https://www.postgresql.org/message-id/ab1YPhD9XNwQH7Kn@nathan) |
| 7 | .NET / .NET Framework | 2026年4月サービシングリリース (4/14) | リモートコード実行 (CVE-2026-32178)、DoS (CVE-2026-32203, CVE-2026-32226) 等の複数セキュリティ脆弱性修正 | [.NET Blog](https://devblogs.microsoft.com/dotnet/dotnet-and-dotnet-framework-april-2026-servicing-updates/) |
| 8 | Zed Editor | 週次リリース (4月第2週) | エージェントスレッドのトップダウンストリーミング、ネイティブ devcontainer 対応、ファイルファインダーの順序非依存マッチング、Focus Follows Mouse | [Releases](https://zed.dev/releases/stable) |
| 9 | Deno | 新バージョン (4/9) | MIMEType サポート、Windows での追加シグナル対応、OTEL 属性の配列値対応、`--cpu-prof-flamegraph` フラグで SVG フレームグラフ生成 | [GitHub Releases](https://github.com/denoland/deno/releases) |
| 10 | Rust for CPython | 進捗レポート (4月) | CPython への Rust 統合プロジェクトが Python 3.16 をターゲットに決定。全テスト済みプラットフォームで CI ビルド成功、Rust チームとの API 設計議論が進行中 | [Python Insider](https://blog.python.org/2026/04/rust-for-cpython-2026-04/) |

## Deep Dive

- [Kubernetes v1.36 — GA 機能・削除・注目の新機能](./tu-kubernetes-1-36.md)
- [TypeScript 7.0 (tsgo) — Go ベース新コンパイラの現状と移行ガイド](./tu-typescript-7-tsgo.md)
