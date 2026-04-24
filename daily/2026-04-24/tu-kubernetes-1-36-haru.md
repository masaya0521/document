# Kubernetes v1.36 "Haru" — User Namespaces GA と OCI VolumeSource

- **日付**: 2026-04-22
- **カテゴリ**: DB・Infra
- **ソース**: [Kubernetes v1.36: ハル (Haru) — Kubernetes Blog](https://kubernetes.io/blog/2026/04/22/kubernetes-v1-36-release/), [Kubernetes v1.36 Release (April-22–2026) — Medium](https://medium.com/@gokulsrinivas.b/kubernetes-v1-36-less-about-new-features-more-about-what-works-9c01f929f21d)

## 概要

Kubernetes v1.36 "Haru"（春）が 2026-04-22 に公開されました。70 件の機能強化（Stable 18 / Beta 25 / Alpha 25）を含み、1 月 12 日から 4 月 22 日までの 15 週間のリリースサイクルに 106 社 491 名が貢献しています。目玉は、セキュリティ関連で長年議論されてきた **User Namespaces の GA** と、AI / ML ワークロードに刺さる **OCI VolumeSource の GA**、そして `gitRepo` / `IPVS kube-proxy` の削除です。

「機能追加」より「ハードニングと削除」に寄った堅実なリリースで、本番運用しているクラスタ管理者は削除項目の影響調査が必須です。

## 主な変更点

### Stable（GA）に昇格した主要機能

**User Namespaces（`hostUsers: false`）**
- Pod 内の root をホストの非特権ユーザにマッピングする defense-in-depth 機能
- コンテナエスケープが起きてもホスト特権につながらないため、マルチテナントや SaaS コントロールプレーン向けに効く
- `hostUsers: false` を Pod spec に書くだけで有効化可能

**OCI Artifact / Image Volume Source**
- 任意の OCI イメージを Volume として参照し、kubelet がレジストリから pull してマウントする
- モデルウェイト、設定ファイル、データセット、バイナリツールなどを OCI artifact として配布・バージョン管理できる
- AI / ML のモデル配布が従来の `initContainer` ダウンロードや PV プリロードから OCI ベースに統一できる

**MutatingAdmissionPolicy**
- CEL（Common Expression Language）でミューテーションロジックを宣言的に記述可能
- 従来の webhook 実装を Kubernetes ネイティブオブジェクトに置き換えられ、外部サービス依存を減らせる
- 高性能な代替手段としてデフォルト有効

**SELinux Volume Mounting の全面有効化**
- Volume 全体の再帰的なリラベルの代わりに `mount -o context=XYZ` を使用
- 大容量 Volume のマウント時間を大きく短縮

**Fine-Grained Kubelet API Authorization**
- kubelet の HTTPS API に対する最小権限アクセス制御が可能に

### Beta に昇格した主要機能

**HPA Scale-to-Zero**
- `HPAScaleToZero` が Beta 化しデフォルト有効に。Object / External メトリクスを使う HPA が 0 レプリカへスケール可能
- イベント駆動・バッチ系ワークロードのアイドルコスト削減に直結

**Dynamic Resource Allocation（DRA）関連**
- Partitionable Devices、Consumable Capacity、Device Taints/Tolerations が Beta 化
- GPU シェアリングや MIG パーティショニング、量子アクセラレータ等の「特殊デバイス抽象化」が実用段階に

## 破壊的変更・移行ガイド

削除・廃止項目は既存マニフェストを壊す可能性があるため、アップグレード前に必ず確認が必要です。

- **`gitRepo` Volume の完全無効化**: セキュリティリスクのため削除。使っている場合は initContainer + emptyDir への書き換え、もしくは OCI VolumeSource への置換を検討
- **`IPVS` モード（kube-proxy）の削除**: v1.35 で deprecation、v1.36 で削除。`nftables` または `iptables` に移行する必要がある。Service 数が多い環境は性能特性の違いに注意
- **Service の `externalIPs` フィールド deprecation**: v1.43 での削除予定。LoadBalancer または MetalLB 等への移行計画を立てる
- **Ingress NGINX の廃止**: 2026-03-24 付で SIG Network と Security Response Committee が正式にプロジェクト終了。以降、バグ修正 / CVE 対応は一切行われない。InGate、ingress-nginx の他実装、Gateway API 実装（Envoy Gateway, Cilium 等）への移行計画が急務

## 今後の注目点

- **Ingress NGINX からの移行**: Production クラスタで最優先の課題。Gateway API への統一が現実解になりつつある
- **AI ワークロード強化**: OCI VolumeSource + DRA Beta で「モデル配布 × GPU 抽象化」のエンドツーエンドが整う。推論プラットフォームのリファレンス実装が各社から出てくる時期
- **User Namespaces のデフォルト化**: GA してもまだオプトイン。主要 PaaS（EKS / GKE / AKS）での採用状況と、CNI / CSI プラグイン側の互換性検証を追うのが有効
- **v1.37 に向けて**: Kubernetes の次期リリースは 2026 年 8 月予定。DRA 周りの Stable 化とネットワーク API 整理が焦点
