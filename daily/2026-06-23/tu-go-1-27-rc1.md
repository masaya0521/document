# Go — 1.27 Release Candidate 1

- **日付**: 2026-06-23
- **カテゴリ**: Language
- **ソース**: [golang-announce (RC1)](https://groups.google.com/g/golang-announce/c/Cu9HkstbtpA/m/NfBgswyTBgAJ), [Go 1.27 Release Notes (draft)](https://go.dev/doc/go1.27)

## 概要

2026年6月19日、Go 1.27 の Release Candidate 1 が公開された。正式版は例年のスケジュール通り8月リリースが見込まれている。本リリースは「見た目以上に大きい」と評される通り、長らく要望が多かった**ジェネリックメソッド**の解禁という言語仕様の根幹に関わる変更を含み、加えて `encoding/json/v2` の新実装、ポスト量子暗号（ML-DSA）の標準化、ランタイムのアロケーション最適化など、実務に直接効く改善が幅広く盛り込まれている。

RC 段階のため、本番ワークロードでの負荷テストやユニットテストでの検証が呼びかけられている。`go install golang.org/dl/go1.27rc1@latest` で導入できる。

## 主な変更点

### 言語仕様：ジェネリックメソッド

最大の目玉。これまでメソッドは独自の型パラメータを宣言できず、ジェネリックな振る舞いはパッケージスコープの関数として書くしかなかった。1.27 ではメソッド宣言自身が型パラメータを持てるようになり、特定の型の名前空間にジェネリックな操作を所属させられる。

```go
// メソッドが独自の型パラメータ U を宣言できる
func (t T) GenericMethod[U any](u U) { /* ... */ }
```

ただし制約もある。インターフェースのメソッドは型パラメータを宣言できず、またインターフェースメソッドをジェネリックメソッドで実装することもできない。

その他の言語仕様変更:

- **構造体リテラルのキー**: 任意の有効なフィールドセレクタを使用可能に（トップレベルのフィールド名に限定されなくなった）
- **関数型推論の一般化**: ジェネリック関数を一致する関数型の変数へ代入・変換するあらゆる文脈で型推論が効くように

### 標準ライブラリ：encoding/json/v2

新実装の `encoding/json/v2` パッケージが追加。厳密な UTF-8 チェックや JSON 内の重複キー検出を備え、Marshal は従来同等、Unmarshal は大幅な性能改善を実現する。

その他の標準ライブラリ追加:

- **crypto/mldsa**: FIPS 204 ML-DSA に対応した新パッケージ。`crypto/tls` も ML-DSA 署名・MLKEM1024 鍵交換をサポートし、ポスト量子暗号への移行が進む
- **simd / simd/archsimd**（実験的）: ハードウェア非依存の可搬 SIMD サポート。arm64・amd64・WebAssembly で 128bit 拡張に対応
- **bytes.CutLast / strings.CutLast**: 末尾の区切り文字でスライス
- **math/big.Int.Divide**: 複数の丸めモードに対応した除算・剰余
- UUID 生成・パース用の新パッケージ
- `unicode` を Unicode 17 に更新

### ランタイム・パフォーマンス

- **小サイズアロケーションの高速化**: 80 バイト未満の一部メモリ割り当てコストを最大30%削減。バイナリサイズは約60KB増だが、全体で約1%の性能向上を見込む
- **goroutineleak プロファイル**: ガベージコレクタを活用して goroutine リークを検出する新プロファイルタイプを正式サポート
- runtime/pprof の goroutine ラベルをヘッダ行に出力するなどトレースバックを改善

### ツールチェーン

- **レスポンスファイル対応**: `compile`・`link`・`asm`・`cgo`・`cover`・`pack` で GCC 互換の `@file` パースをサポート
- **go test**: `stdversion` vet チェックがデフォルト有効化（バージョン不適合なシンボル使用を検出）。`-json` に `OutputType` フィールド追加
- **go doc**: `go doc example.com/pkg@v1.2.3` 構文と `-ex` フラグに対応
- **go fix**: 新アナライザ（atomictypes・embedlit・slicesbackward・unsafefuncs）を追加、`fmtappendf` は削除
- **go mod tidy**: 重複する `require` ブロックを自動統合

## 破壊的変更・移行ガイド

- **プラットフォームサポート**: Darwin（macOS）は macOS 13 Ventura 以降のみサポート（Go 1.26 で予告済み）。古い macOS 上の CI/ローカル環境は要確認
- **ppc64**: ELFv2 ABI へ移行し、Cgo・PIE・外部リンク対応を追加
- **go fix の fmtappendf 削除**: 当該アナライザに依存していたワークフローは見直しが必要

言語仕様の追加（ジェネリックメソッド・構造体リテラルキー）は後方互換であり、既存コードはそのまま動作する。

## 今後の注目点

- 8月の正式版に向け、ジェネリックメソッドが標準ライブラリ・主要 OSS でどう活用されるか
- `encoding/json/v2` の本番採用と、既存 `encoding/json` からの移行パターンの確立
- ML-DSA を含むポスト量子暗号の TLS スタックへの浸透
- 実験的 `simd` パッケージの安定化ロードマップ
