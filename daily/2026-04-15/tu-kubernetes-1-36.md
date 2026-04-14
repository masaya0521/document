# Kubernetes v1.36 — GA 機能・削除・注目の新機能

- **日付**: 2026-04-22（リリース予定）
- **カテゴリ**: DB・Infra
- **ソース**: [Sneak Peek](https://kubernetes.io/blog/2026/03/30/kubernetes-v1-36-sneak-peek/), [Release Information](https://www.kubernetes.dev/resources/release/)

## 概要

Kubernetes v1.36 は 2026年4月22日にリリース予定のバージョンで、20個の新しいアルファ機能を含む。ワークロードパフォーマンス、API スケーラビリティ、リソース効率の3つの領域に焦点を当てている。特に、Ingress NGINX の引退と Gateway API への移行、gitRepo ボリュームの完全削除など、運用に直接影響する変更が含まれる。

## GA になった主な機能

### SELinux ボリュームラベリング高速化 (KEP-1710)

`mount -o context=XYZ` オプションにより、マウント時にボリューム全体に正しい SELinux ラベルを適用する。従来の再帰的ラベル変更と比較してポッドの起動遅延が大幅に削減される。Kubernetes v1.27 からベータだった機能が安定化。

### MutatingAdmissionPolicy

動的なアドミッションコントロールを宣言的に設定可能にする機能が GA に昇格。

### 外部署名 ServiceAccount トークン

`kube-apiserver` がトークン署名を外部システムに委譲できるようになり、クラウド鍵管理サービス（AWS KMS、GCP Cloud KMS 等）との統合が強化される。

### ユーザー名前空間 (KEP-127)

Pod 内でのユーザー名前空間サポートが安定化。コンテナ内の root をホスト上の非特権ユーザーにマッピングし、セキュリティを強化する。

## ベータに昇格した機能

### DRA デバイス Taint と Toleration

デバイスが tainted とマークされるとスケジューリングで使用されないようにでき、GPU 等の特化ハードウェアの細かい制御が可能になる。

## 注目の新機能（アルファ）

### DRA 分割可能デバイス対応

単一の GPU を複数の論理単位に分割し、複数のワークロードで共有可能にする。AI/ML ワークロードでの GPU リソース効率の向上が期待される。

### ワークロード対応プリエンプション

AI/ML ジョブ向けのワークロード対応プリエンプション機能。ジョブの優先度やリソース要件に基づいたインテリジェントなスケジューリング判断が可能に。

### シャード化 API ストリーム

大規模クラスタ向けに API watch ストリームをシャード化し、API サーバーの負荷を分散する。

## 削除・非推奨化

### gitRepo ボリューム完全削除

v1.36 で `gitRepo` ボリュームドライバが完全に無効化される。root 権限で攻撃者がコード実行可能な脆弱性があったため。代替として `initContainers` で `git clone` を行うパターンを推奨。

### Ingress NGINX 引退

2026年3月24日に Ingress NGINX が正式引退。以降はバグ修正・セキュリティアップデートなし。Gateway API への移行が強く推奨される。

### `service.spec.externalIPs` 非推奨化

セキュリティリスク排除のため非推奨化。v1.43 で削除予定。

## 今後の注目点

- Gateway API がネットワーキングの標準に。Ingress からの移行計画の策定が急務
- DRA 関連機能（分割デバイス、Taint/Toleration）が今後のリリースでベータ・GA に向けて進化
- AI/ML ワークロード向けスケジューリング機能の拡充が継続
