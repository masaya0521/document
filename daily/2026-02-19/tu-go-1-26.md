# Go 1.26 — Green Tea GC・SIMD・言語仕様変更の全容

- **日付**: 2026-02-10
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://go.dev/blog/go1.26), [リリースノート](https://go.dev/doc/go1.26)

## 概要

Go 1.26 は2026年2月10日にリリースされたメジャーバージョンで、Go 1.25 で実験的に導入された Green Tea ガベージコレクタのデフォルト有効化が最大のハイライト。GC オーバーヘッドが10〜40%削減され、cgo 呼び出しも約30%高速化された。言語仕様では `new` 関数の拡張とジェネリック型の自己参照が追加され、標準ライブラリには `crypto/hpke`（量子耐性対応）や実験的 SIMD パッケージなど多数の新機能が含まれる。

## 主な変更点

### 言語仕様の変更

#### `new` 関数の拡張

`new` 関数のオペランドに式を指定して初期値を設定できるようになった。JSON や Protocol Buffers のシリアライゼーションなどで便利。

```go
// Before: 一時変数が必要だった
tmp := yearsSince(born)
Age: &tmp

// After: 直接指定可能
Age: new(yearsSince(born))
```

#### ジェネリック型の自己参照

型パラメータリスト内での自己参照が許可され、複雑なデータ構造やインターフェースの実装が簡潔になった。

```go
type Adder[A Adder[A]] interface {
    Add(A) A
}
```

### ランタイムの改善

#### Green Tea ガベージコレクタ（デフォルト有効化）

- Go 1.25 の実験的機能がデフォルトで有効化
- **GC オーバーヘッドを10〜40%削減**
- Ice Lake / Zen 4 以降の CPU ではベクタ命令を活用し、さらに10%の改善
- `GOEXPERIMENT=nogreentea` で無効化可能

#### cgo 呼び出しの高速化

- ベースラインオーバーヘッドを**約30%削減**

#### ヒープベースアドレスのランダム化

- 64ビット環境でセキュリティ強化のため実装
- `GOEXPERIMENT=norandomizedheapbase64` で無効化可能

#### ゴルーチンリークプロファイル（実験的）

- `GOEXPERIMENT=goroutineleakprofile` で有効化
- ブロック状態で永久に起動しないゴルーチンを検出

### ツールチェインの改善

#### `go fix` コマンドの完全改修

- 最新のイディオムへの自動更新機能を搭載
- 数十の fixer とソースレベルのインライナーを内蔵
- `go vet` と同じ解析フレームワークを使用

#### プロファイラの改善

- `pprof` の Web トップページがデフォルトでフレームグラフ表示に変更

### 標準ライブラリの新機能

| パッケージ | 追加機能 |
|----------|--------|
| `crypto/hpke` | HPKE (RFC 9180) 実装、量子耐性対応 |
| `simd/archsimd` | アーキテクチャ固有の SIMD 操作（実験的） |
| `runtime/secret` | 秘密情報のセキュアな消去機構 |
| `bytes` | `Buffer.Peek()` メソッド |
| `errors` | `AsType()` ジェネリック関数 |
| `reflect` | `Fields()`, `Methods()` イテレータ |
| `io` | `ReadAll()` が2倍高速化・メモリ使用量削減 |
| `testing` | `ArtifactDir()` メソッド |

### TLS / 暗号関連

- **ML-KEM ハイブリッド鍵交換がデフォルト有効化**（`SecP256r1MLKEM768`, `SecP384r1MLKEM1024`）
- `crypto/dsa`, `crypto/ecdsa`, `crypto/rsa` 等でランダム性パラメータが無視され、常に暗号学的に安全な値を使用

### コンパイラ / リンカ

- スライスのバッキングストアをスタック上に割り当て可能なケースが増加（パフォーマンス向上）
- Windows/arm64: cgo 内部リンクモード対応

## 破壊的変更・移行ガイド

### サポート終了予定

- **macOS**: Go 1.26 は macOS 12 Monterey 対応の最終版。Go 1.27 は macOS 13 以上が必須
- **Windows**: 32ビット ARM (`windows/arm`) ポートは削除済み
- **PowerPC**: ELFv1 ABI 対応が最終版（Go 1.27 から ELFv2 へ移行）

### GODEBUG 設定の削除予定（Go 1.27）

以下の設定は Go 1.27 で削除予定：
- `tlsunsafeekm`, `tlsrsakex`, `tls10server`, `tls3des`
- `x509keypairleaf`, `asynctimerchan`

### ブートストラップ要件

- Go 1.26 のビルドには Go 1.24.6 以上が必要
- Go 1.28 のビルドには Go 1.26 の小版以上が必要

## 今後の注目点

- Green Tea GC の実環境でのパフォーマンス影響（特にレイテンシの改善度合い）
- `simd/archsimd` パッケージの安定化と対応アーキテクチャの拡充
- ML-KEM 対応による量子耐性 TLS の普及動向
- Go 1.27 でのサポート終了（macOS 12、ELFv1）に向けた移行準備
