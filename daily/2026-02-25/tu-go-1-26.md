# Go 1.26 — ポスト量子暗号・SIMD サポートと言語改善

- **日付**: 2026-02-10
- **カテゴリ**: Language
- **ソース**: [公式ブログ](https://go.dev/blog/go1.26), [リリースノート](https://go.dev/doc/go1.26)

## 概要

Go 1.26 は Go 1.25 のリリースから 6 ヶ月後にリリースされた。言語仕様の変更（`new()` の拡張、ジェネリック型の自己参照）、Green Tea GC のデフォルト有効化による GC オーバーヘッドの 10〜40% 削減、ポスト量子暗号対応の `crypto/hpke` パッケージ、実験的 SIMD サポートなど、パフォーマンスとセキュリティの両面で大きな進展がある。

## 主な変更点

### 言語仕様の変更

#### `new()` 関数の拡張

`new` 関数が初期値を受け取れるようになった。これにより、ポインタベースのオプション値を簡潔に表現できる。

```go
// 従来
age := yearsSince(born)
ptr := &age

// Go 1.26
ptr := new(yearsSince(born))

// JSON シリアライゼーションでの活用
type Person struct {
    Name string  `json:"name"`
    Age  *int    `json:"age,omitempty"`
}

p := Person{
    Name: "Alice",
    Age:  new(30),  // ポインタを簡潔に生成
}
```

#### ジェネリック型の自己参照

ジェネリック型がその型パラメータリスト内で自身を参照可能になった。これにより、再帰的なデータ構造の型定義がより自然に書ける。

### パフォーマンス改善

#### Green Tea GC（デフォルト有効化）

新しいガベージコレクタ「Green Tea GC」がデフォルトで有効化された。小オブジェクトのマーキング・スキャンが改善され、GC オーバーヘッドが **10〜40% 削減** される。

#### cgo オーバーヘッド削減

cgo 呼び出しのベースラインオーバーヘッドが **約 30% 削減**。C ライブラリとの連携が多いプロジェクトで恩恵がある。

#### その他

- **`io.ReadAll`**: 約 2 倍高速化、メモリ使用量 50% 削減
- **`image/jpeg` コーデック**: 新実装で大幅な高速化
- **スライス最適化**: コンパイラがスタック上にメモリ確保する場面を拡大

### 新パッケージ

#### `crypto/hpke` — Hybrid Public Key Encryption

RFC 9180 準拠の HPKE 実装。ポスト量子ハイブリッド KEM をサポートし、公開鍵ベースの暗号化を安全に行える。

#### `crypto/mlkem/mlkemtest`, `testing/cryptotest`

暗号プリミティブのテスト支援パッケージ。

### 実験的機能

#### SIMD サポート（`simd/archsimd`）

`GOEXPERIMENT=simd` で有効化。AMD64 上で 128/256/512 ビットベクトル型（`Int8x16`, `Float64x8` 等）を提供。高性能な数値計算やデータ処理に活用できる。

#### `runtime/secret`

暗号処理時の機密データ（鍵、トークン等）の安全な消去を提供。レジスタ、スタック、ヒープメモリを使用後にクリアする。AMD64/ARM64 Linux で利用可能。

#### Goroutine リークプロファイル

`GOEXPERIMENT=goroutineleakprofile` で有効化。`/debug/pprof/goroutineleak` エンドポイントで、永遠にブロック状態のゴルーチンを検出できる。

### ツール改善

#### `go fix` コマンドの全面刷新

Go analysis framework を採用し、「modernizers」と呼ばれる数十の fixer を搭載。新しい言語機能やAPI への移行を自動提案・適用する。`//go:fix inline` ディレクティブによるインライン展開にも対応。

#### `go mod init` の変更

デフォルトで N-1 バージョンを指定するようになり、互換性が向上。

### 標準ライブラリの改善

- **`bytes.Buffer.Peek`**: バッファ位置を進めない読み取り
- **`net` パッケージ**: `DialIP`, `DialTCP`, `DialUDP`, `DialUnix` がコンテキスト対応
- **`reflect` パッケージ**: `Fields`, `Methods`, `Ins`, `Outs`, `Value.Fields` 等の反復メソッド追加

## 今後の注目点

- **Green Tea GC の安定化**: 大規模本番環境でのベンチマーク結果に注目
- **SIMD の安定化**: 現在は AMD64 のみだが、ARM64 への拡張が期待される
- **ポスト量子暗号**: `crypto/hpke` の実践的な活用パターンの蓄積
- **Go 1.27**（2026 年 8 月予定）: SIMD の安定化やさらなる言語改善が見込まれる
