# Deno 2.6 — dx, tsgo, deno audit で開発体験を大幅強化

- **日付**: 2026-02-17
- **カテゴリ**: Backend / Runtime
- **ソース**: [公式ブログ](https://deno.com/blog/v2.6), [GitHub Release](https://github.com/denoland/deno/releases/tag/v2.6.0)

## 概要

Deno 2.6 は、パッケージバイナリ実行ツール `dx`、Go 実装の型チェッカー `tsgo` 統合、依存関係セキュリティ監査コマンド `deno audit` など、開発体験を大幅に向上させる多数の新機能を含むリリースである。権限システムの細粒度化やセキュリティ関連機能の強化も特筆すべき点で、Node.js 互換性もさらに改善されている。

## 主な変更点

### dx — npx の代替ツール

npm および JSR パッケージのバイナリを手軽に実行できる新コマンド `dx` が導入された。

```bash
# npm パッケージのバイナリを実行
dx create-next-app my-app

# JSR パッケージも対応
dx jsr:@std/cli my-tool
```

- デフォルトで `--allow-all` 権限を適用
- ダウンロード前にプロンプトを表示
- ライフサイクルスクリプトを自動実行
- `deno x --install-alias` でエイリアスをインストール可能

### tsgo による高速型チェック

Go で記述された TypeScript の新しい実験的型チェッカー `tsgo` が統合された。

```bash
deno check --unstable-tsgo main.ts

# または環境変数で有効化
DENO_UNSTABLE_TSGO=1 deno check main.ts
```

- 内部プロジェクトで **約2倍の速度改善** を実現
- `compilerOptions.paths` の正確なモジュール解決
- `skipLibCheck` や `isolatedDeclarations` などの高度な設定をサポート

### deno audit — 依存関係のセキュリティ監査

```bash
# GitHub CVE データベースでチェック
deno audit

# Socket.dev の脆弱性データベースも統合
deno audit --socket
```

### より細粒度な権限制御

新しいフラグで権限をより細かく制御可能に。

```bash
# 特定パスの読み取りを無視（NotCapable ではなく NotFound を返す）
deno run --ignore-read=/etc main.ts

# 特定の環境変数を隠蔽（undefined を返す）
deno run --ignore-env=AWS_SECRET_KEY main.ts
```

**Permission Broker（実験的）**: 別プロセスで権限リクエストを管理する仕組み。

```bash
DENO_PERMISSION_BROKER_PATH=/perm_broker.sock deno run untrusted_code.ts
```

### 依存管理の強化

- **`deno approve-scripts`**: ライフサイクルスクリプト実行パッケージの選択的承認
- **`minimumDependencyAge`**: 新規公開パッケージを回避するための最小年齢設定

```json
{
  "minimumDependencyAge": "120"
}
```

- **`--lockfile-only`**: パッケージダウンロードなしでロックファイルのみ更新

### Source Phase Imports（Wasm サポート強化）

```typescript
import source addModule from "./add.wasm";
const addInstance = WebAssembly.instantiate(addModule);
```

### その他の改善

- **BroadcastChannel API** が実験段階から安定版へ
- **`--require` フラグ**: CommonJS モジュールのプリロード対応
- **`@types/node` 自動包含**: 手動インストール不要に
- **V8 14.2 アップグレード**
- **ネイティブソースマップサポート**
- **テストカバレッジ**: ワーカーからのデータ収集に対応

## 破壊的変更・移行ガイド

- `deno install -g` でスクリプトに引数を渡す場合は `--` セパレータが必須に

```bash
# Before
deno install -g --name my-tool main.ts --port 3000

# After
deno install -g --name my-tool main.ts -- --port 3000
```

## 今後の注目点

- **tsgo の安定化**: 現在は `--unstable-tsgo` フラグが必要だが、将来的にデフォルトの型チェッカーとなる可能性
- **Permission Broker の発展**: セキュリティモデルのさらなる進化として、サードパーティコードの権限管理がより柔軟に
- **Deno Sandbox / Deno Deploy**: 2月に一般提供開始された Deno Deploy や Deno Sandbox との統合強化
- **Node.js 互換性**: 暗号化・ファイルシステム・SQLite 等の互換性改善が継続
