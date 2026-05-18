# Pwn2Own Berlin 2026 — 47 件のゼロデイが示すクライアント / OS / AI の地殻変動

- **日付**: 2026-05-19
- **カテゴリ**: Tech
- **ソース**: [BleepingComputer](https://www.bleepingcomputer.com/news/security/hackers-earn-1-298-250-for-47-zero-days-at-pwn2own-berlin-2026/) / [Cybersecurity News](https://cybersecuritynews.com/pwn2own-berlin-2026/) / [Security Affairs](https://securityaffairs.com/192183/hacking/pwn2own-berlin-2026-day-one-523000-paid-out-ai-products-fall.html) / [Windows Forum](https://windowsforum.com/threads/pwn2own-berlin-2026-edge-windows-11-and-ai-gpu-tools-exposed.418464/)

## 概要

OffensiveCon 併催の Pwn2Own Berlin 2026 が 5/14–16 の 3 日間にわたり開催され、47 件のゼロデイ脆弱性に対し合計 $1,298,250 の賞金が支払われた。今回特筆すべきは、初の AI/ML プラットフォーム部門が新設され**全ターゲットが陥落**した点、そして NVIDIA CUDA や Red Hat Enterprise Linux など「基盤層」に攻撃面が広がった点である。コンシューマ向けブラウザ・OS だけでなく、AI インフラと GPU/HPC スタックがエンタープライズの新しい攻撃面として現れた。

## 詳細

### Day 1: $523,000、Edge / Windows 11 / LiteLLM が陥落

初日だけで 24 件のユニーク脆弱性が確認され、合計 $523,000 が支払われた。

- **Microsoft Edge**: DEVCORE Research Team の Orange Tsai が **4 つのロジックバグをチェイン** して Edge サンドボックスを脱出。一発で $175,000 + Master of Pwn 17.5 ポイントを獲得した。ロジックバグの連鎖はメモリ破壊よりパッチ難度が高いことが多く、Microsoft の Edge セキュリティモデルに構造的な見直しを迫る内容。
- **Windows 11**: DEVCORE の Angelboy / TwinkleStar03 が improper access control を突いた特権昇格に成功。1 日で複数の Windows 11 EoP が確認された。
- **LiteLLM**: 5 万社以上で利用される LLM プロキシ OSS が **3 つの異なるチームに陥落**。k3vg3n の full-chain では SSRF + コードインジェクションを連鎖させ、完全システム掌握まで到達した。

### AI/ML 部門の新設と全敗

Pwn2Own が初導入した AI/ML プラットフォーム部門では、エントリーされた全ターゲットが攻略された。LiteLLM の 3 回の陥落は象徴的で、「LLM をプロダクトに組み込むためのプロキシ層」が、企業が自前で運用する AI インフラの新たな攻撃面として確立されつつあることを示す。 認証バイパス、SSRF、プロンプト経由のサーバ制御など、Web プロキシ系の伝統的な弱点が LLM ゲートウェイに引き継がれている。

### NVIDIA CUDA / GPU カーネル領域への侵入

Team Reverie は NVIDIA CUDA Toolkit 12.8 の `nvvmCompileProgram` における heap overflow を突き、悪意ある PTX (Parallel Thread Execution) コードからカーネルモード実行に到達した。「悪意のあるデータセット → GPU ドライバ → ホストカーネル」というルートは、AI 訓練パイプラインの **データ供給チェーン全体が攻撃面**であることを意味する。共有 GPU クラスタを運用する企業にとっては、データ受け入れと PTX 検証の境界設計が新しい必須要件になる。

### Red Hat / Linux 側の動向

Red Hat Enterprise Linux に対する exploit も成立しており、Windows 一辺倒だった Pwn2Own のターゲット構成が、エンタープライズ Linux と AI/GPU 基盤に大きくシフトしているのが今回のメッセージである。

## 今後の注目点

- **AI プロキシ層 (LiteLLM 等) のサプライチェーン強化**: SBOM・依存リスト管理だけでなく、prompt 経由の SSRF 防御、関数呼び出しの allow-list が一般化するか。
- **GPU/HPC スタックの脅威モデル更新**: 「データ → コンパイラ → カーネル」攻撃面に対し、ML データセットの署名検証や PTX サニタイズの運用が広がる可能性。
- **Edge と Chromium 双方への波及**: Orange Tsai のロジックチェーンは Chromium ベース全体に共通する可能性があり、サンドボックス境界の再設計が見込まれる。
- **CISA KEV への登録ペース**: 47 件のうち、いつどれが KEV に追加されるか。同時期に Cisco SD-WAN の CVE-2026-20182 も追加されており、エンタープライズのパッチ運用が再び忙しくなる。
- **Pwn2Own の AI 部門の継続性**: Initial 部門に全勝報酬が支払われた以上、来年は対象が Anthropic 自社製ホスティング・LangChain・vLLM などに広がる流れが見込まれる。
