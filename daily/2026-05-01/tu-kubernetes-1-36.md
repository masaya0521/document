# Kubernetes v1.36 — DRA 強化と ServiceAccount トークン外部署名

- **日付**: 2026-05-01
- **カテゴリ**: DB・Infra
- **ソース**: [Kubernetes v1.36 Sneak Peek (公式ブログ)](https://kubernetes.io/blog/2026/03/30/kubernetes-v1-36-sneak-peek/), [Kubernetes Releases](https://kubernetes.io/releases/), [Kubernetes Contributors: v1.36 Release Information](https://www.kubernetes.dev/resources/release/)

## 概要

Kubernetes v1.36 は 2026-04-22 にリリース。前バージョン (1.35 Timbernetes) 以降の Dynamic Resource Allocation (DRA) 強化、SELinux ボリュームラベリングの GA、ServiceAccount トークンの外部署名対応など、主に **セキュリティとリソース管理の堅牢化** にフォーカスしたリリース。同時に長らく放置されていた `gitRepo` ボリュームのような古い API/機能を恒久無効化する整理も入っている。

## 主な変更点

### SELinux ボリュームラベリング高速化（GA）
- マウント時にカーネルへ SELinux ラベルを直接適用するパス（`mount -o context=`）を GA に昇格。
- 大量ファイルを抱える PV のラベル付けでフルスキャンが不要になり、ポッドの起動遅延が大幅に短縮。
- セキュリティと起動性能のトレードオフが解消し、SELinux 強制環境のクラスタが本番採用しやすくなる。

### ServiceAccount トークンの外部署名
- ServiceAccount JWT の署名鍵を Kubernetes API サーバ外部の **KMS / HSM** に委譲できるように。
- Cloud KMS、Hardware Security Module、AWS KMS、Google Cloud KMS、Azure Key Vault といった既存の鍵管理基盤と統合可能。
- 鍵の物理的な保護とローテーション戦略を運用基盤側に寄せられ、コンプライアンス要件 (FIPS, FedRAMP 等) との親和性が向上。

### Dynamic Resource Allocation (DRA) 強化
- **Device Taints と Tolerations（Beta）**: GPU や専用デバイスを node taints と同じモデルで制御可能。利用可能なポッドだけを許容できる。
- **分割可能デバイス対応**: 物理的に共有できるデバイス（例: MIG 構成済 GPU など）を複数ワークロードで分割利用するためのスキーマ整備。
- AI/ML やゲーム配信のような GPU 集約ワークロードを Kubernetes で素直に表現できるようになる方向性。

### 廃止・削除
- **`gitRepo` ボリュームドライバー**: v1.36 で永久無効化。代替は init container での clone か、CSI 経由のリポジトリマウント。
- **`externalIPs` フィールド**: v1.43 での完全削除を予定。代替手段（LoadBalancer/Ingress）への移行を促す。

## 破壊的変更・移行ガイド

### `gitRepo` を使っているマニフェストの置き換え

```yaml
# v1.35 まで
volumes:
  - name: src
    gitRepo:
      repository: https://github.com/example/repo
      revision: main
```

→ init container 方式へ:

```yaml
volumes:
  - name: src
    emptyDir: {}
initContainers:
  - name: clone
    image: alpine/git
    args: ["clone", "--depth=1", "https://github.com/example/repo", "/src"]
    volumeMounts:
      - name: src
        mountPath: /src
```

### `externalIPs` 利用の点検
- v1.36 の段階では非推奨警告に留まるが、v1.43 で完全削除されるため、長期運用するクラスタでは早期に Ingress/LoadBalancer 等へ移行を進めるのが安全。

### ServiceAccount 署名鍵の外部化
- API サーバの起動フラグに外部署名プロバイダ設定を追加するだけで段階的に切り替え可能（既存の内蔵署名と並行運用するモードあり）。
- 鍵ローテーションは API サーバの再起動を伴わない手順が用意される予定。

## 今後の注目点

- DRA の **Device Taints/Tolerations** がベータからどれだけ早く GA に進むか。GPU 共有型ワークロードのデフォルト経路になるかが焦点。
- v1.36 + v1.37 で予定されている DRA の structured parameters 周りの整理が、デバイスベンダー（NVIDIA, AMD, Intel 等）のドライバ実装にどう波及するか。
- `gitRepo` 廃止のように、長らく「使われ続けている」が攻撃面として残っていた API の整理がどこまで進むか（次に槍玉に上がるのは `hostPath` の静的 PV や非 CSI なドライバなど）。
- ServiceAccount トークン外部署名と、最近進んでいる **Workload Identity Federation 統合**との接続点。
