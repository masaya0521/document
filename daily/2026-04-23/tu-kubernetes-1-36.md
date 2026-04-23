# Kubernetes v1.36 — Stability・Compatibility・Reproducibility 重視のリリース

- **日付**: 2026-04-23（リリース日: 2026-04-22）
- **カテゴリ**: DB・Infra
- **ソース**: [Kubernetes Blog (Sneak Peek)](https://kubernetes.io/blog/2026/03/30/kubernetes-v1-36-sneak-peek/), [Kubernetes Release Info](https://www.kubernetes.dev/resources/release/), [Cloud Native Now 解説記事](https://cloudnativenow.com/features/kubernetes-v1-36-promotes-stability-compatibility-reproducibility/)

## 概要

Kubernetes v1.36 は 2026-04-22 にリリースされた。約80件の Enhancement（うち18件が Stable、18件が Beta、26件が新規 Alpha）を含み、リリース名は "Timbernetes" の系譜を継ぐ流れで、テーマは「派手な新機能よりも安定性・互換性・再現性」。長らく Beta だった機能が一気に GA したのが今回の特徴で、Pod 起動性能・ノードセキュリティ・Admission・GPU 共有といった本番運用上のコア領域が成熟したリリースになっている。

## 主な変更点

### Stable（GA）に昇格した主要機能

- **User Namespaces**: コンテナをルートレスで動かすための仕組みが Kubernetes ネイティブで GA。コンテナ内 UID/GID をホストとマッピング切り離しでき、コンテナ脱出時の影響を大幅に縮小できる。
- **MutatingAdmissionPolicy（GA・デフォルト有効）**: これまで Webhook サーバを別運用するのが一般的だった「リソースの自動変更」を、CEL ベースの宣言的ポリシーとして Kubernetes オブジェクトで表現できる。Admission の運用がよりインフラ寄りに統合される。
- **OCI VolumeSource**: 任意の OCI イメージをボリュームとしてマウント可能に。コンテナイメージと同じ供給網（レジストリ・署名・キャッシュ）でモデル・設定・WASM などをそのまま配布できるようになり、サイドカー無しでアセット配布できるパターンが広がる。
- **HPA Scale-to-Zero**: HPA が active な metric が無いときにレプリカを 0 まで縮退できるようになった。これまで KEDA など外部に頼っていた「アイドル時の完全停止」がコア機能で実現する。
- **Fine-grained Kubelet API Authorization**: kubelet API の認可を細粒度で制御できるようになり、ノードレベルの権限分離が一段進んだ。
- **Faster SELinux labeling for volumes**: 再帰的なラベリングから `mount -o context=XYZ` ベースに置き換え、SELinux 環境での Pod 起動時間を短縮。
- **External signing of ServiceAccount tokens**: 外部 KMS と連携して ServiceAccount トークンに署名可能。

### Beta に昇格

- **DRA: Device Taints/Tolerations**: 特殊ハードウェアに taint を付与し、専用の Pod だけが利用できるようにする。GPU/NIC 等の共有戦略を Kubernetes ネイティブで表現できる。
- **DRA: Partitionable Devices**: 1台の GPU を複数の論理デバイスに分割して個別に Pod へ割り当て可能。MIG/MPS 系のシナリオを標準で扱えるようになる。

### Deprecation・Removal

- **削除**: `gitRepo` ボリュームプラグイン（v1.11 から非推奨。深刻なセキュリティリスクのため）。
- **削除**: kube-proxy の **IPVS モード**（v1.35 で deprecated）。`nftables` モードへの移行が必要。
- **Deprecation**: Service の `.spec.externalIPs`（中間者攻撃の経路になり得るため）。完全削除は v1.43 を予定。
- **エコシステム**: Ingress-NGINX は SIG Security の判断で 2026-03-24 に retire。後継の選択（Gateway API / 商用 Ingress / Envoy 系）が必要。

## 破壊的変更・移行ガイド

- `gitRepo` を使っているマニフェストはそのままだと Pod が起動しなくなる。**init コンテナで `git clone` → emptyDir に展開**する形か、CSI ベースの方式に置き換える。
- kube-proxy を IPVS で運用しているクラスタは `--proxy-mode=nftables`（または iptables）に切り替える。`kube-proxy` の起動オプションだけでなく、依存していた IPVS 固有の挙動（一部のスケジューリングアルゴリズム）も再評価が必要。
- Service の `externalIPs` を使っているマニフェストは Deprecation 警告が出るうちに、LoadBalancer / NodePort / Gateway API に寄せておく。
- Ingress-NGINX を使っているクラスタは、**EOL であることを前提**に早期に移行先（Gateway API や商用 Ingress）を選定する。

## 今後の注目点

- **DRA の本格運用**: GPU/NPU の共有が Kubernetes コアで成熟しつつあるので、AI ワークロード向けクラスタ設計が「DRA 前提」に切り替わっていく。次の v1.37 サイクルで Stable 化が進むか要観察。
- **Admission の宣言化**: MutatingAdmissionPolicy GA で、OPA/Kyverno など外部 Webhook の使い分け（コア機能で十分か、外部ポリシーエンジンが要るか）を再整理するタイミング。
- **Scale-to-Zero × Serverless**: HPA Scale-to-Zero が GA したことで、Knative や独自の Serverless レイヤを薄くできる可能性がある。コールドスタート要件と合わせて選定し直す価値がある。
- **Ingress-NGINX 後継**: 2026 年中はクラスタごとに Gateway API への移行が大きなテーマになりそう。
