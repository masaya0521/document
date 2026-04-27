# Kubernetes v1.36 "Haru" — ユーザーネームスペース・OCI ボリューム GA とプロダクション向け新機能

- **日付**: 2026-04-28
- **カテゴリ**: DB・Infra（Kubernetes）
- **ソース**: [Kubernetes v1.36: Haru — Kubernetes Blog](https://kubernetes.io/blog/2026/04/22/kubernetes-v1-36-release/) / [v1.36 Sneak Peek](https://kubernetes.io/blog/2026/03/30/kubernetes-v1-36-sneak-peek/)

## 概要

Kubernetes v1.36 "Haru"（ハル）が 2026-04-22 にリリースされた。リリース名は葛飾北斎『富嶽三十六景』の「赤富士」に由来する。70 機能強化（Stable 18 / Beta 25 / Alpha 25）が含まれ、運用面ではユーザーネームスペースのコンテナ脱出耐性、OCI レジストリから直接マウントできる OCI ボリュームソース、SSH なしで Node ログを覗ける Node ログ検索、Webhook 不要の CEL ベース mutation など、長らく beta だった機能が一斉に GA に到達した。一方で `gitRepo` ボリュームは v1.36 から完全に無効化され、Service の `externalIPs` は v1.43 で削除予定として明記された。本リリースは "セキュリティ既定値の強化" と "オブザーバビリティの底上げ"が大きなテーマとなっている。

## 主な変更点

### Stable 昇格の主要機能

- **きめ細かい kubelet API 認可**: kubelet API のサブリソース単位で認可を分割。`kubectl exec` / `logs` / `portforward` 等の権限分離が可能に
- **ユーザーネームスペース対応**: コンテナ内 root をホストの非特権 UID にマッピング。コンテナ脱出時の被害を限定する追加防御層
- **OCI ボリュームソース**: OCI レジストリのアーティファクトを直接 Volume としてマウント。モデルファイルや設定の配布で `initContainer` + `emptyDir` の合わせ技を不要に
- **変異する管理ポリシー (Mutating Admission Policy)**: CEL で記述する宣言的 mutation。Webhook サーバ運用が不要になり、`MutatingWebhookConfiguration` 比でレイテンシも下がる
- **Node ログ検索**: kubelet 経由で Node のシステムログを取得可能。SSH を開けない環境での障害解析が劇的に楽になる
- **ボリュームグループスナップショット**: 複数 PVC を一貫したスナップショットとして取得。データベース等のマルチボリューム構成で整合性確保
- **外部署名による ServiceAccount トークン**: AWS IAM／GCP IAM／HashiCorp Vault 等を署名者として組み込み可能
- **DRA ガバナンス機能**: Dynamic Resource Allocation が GPU 共有のプロダクション運用に耐える成熟度に到達

### Beta 昇格の主要機能

- **ワークロード対応スケジューリング (WAS)**: Pod グループ単位の原子的スケジューリング。バッチ／ML 学習で「全部スケジュールできるかゼロか」を保証
- **リソースヘルス状態**: GPU 等のデバイス障害を Pod ステータスから可視化
- **制約付き偽装 (Constrained Impersonation)**: 最小権限原則に沿った impersonation。許可された対象にのみ偽装可能
- **DRA 拡張**: GPU 分割（partitionable devices）・キャパシティ共有

### Alpha 新機能（抜粋）

- **HPA Scale-to-Zero**: キューイングシステムと連携して Pod 数 0 まで縮退可能。コスト最適化のための長年の要望
- **CRI リストストリーミング**: 大量コンテナ環境での kubelet メモリ圧力を緩和
- **マニフェストベース管理コントローラー設定**: admission control の宣言的管理

## 破壊的変更・移行ガイド

### v1.36 で削除されたもの

- **`gitRepo` ボリューム**: v1.11 から deprecated だったが、v1.36 で完全無効化。代替は `initContainer` で `git clone` する古典的パターンか、サードパーティの CSI ドライバ

### 廃止予告

- **Service `spec.externalIPs`**: セキュリティ上の理由で v1.43 完全削除予定。MetalLB／LoadBalancer サービスへの移行を計画する必要あり
- **Ingress NGINX**: 2026-03-24 以降の更新なし。Gateway API ベースの代替（envoy gateway, cilium gateway, ingress-nginx の派生など）への移行を検討

### SELinux ボリュームラベル GA の注意点

ラベル適用がマウント時のコンテキスト適用に切り替わり高速化。ただし**異なる特権レベルの Pod が同一 PVC を共有する構成では Pod 設定の慎重な管理が必須**。共有する場合は `seLinuxChangePolicy: Recursive` を明示するなどの再評価が必要。

## 今後の注目点

- **Service `externalIPs` の代替検証**: v1.43 まで猶予はあるが、利用箇所の棚卸しと移行 PoC を早めに着手する価値あり
- **OCI ボリュームソースの adoption**: モデル配布・設定配布の新しいベストプラクティスになる可能性。Flux／Argo CD のリリース順序設計にも影響
- **DRA 本番運用の事例**: GPU 共有・ベンダー固有デバイス管理の標準が整いつつある。NVIDIA/AMD のプラグイン成熟度の差を含めて追う価値あり
- **Mutating Admission Policy への移行**: 運用中の MutatingWebhook を CEL に置換できるかは個別判定。既存資産が多い組織はパイロット導入から
- **次回リリース**: 1.37 は通常通り 4 ヶ月後（2026 年夏〜秋）想定。Sneak Peek の更新を待つ
