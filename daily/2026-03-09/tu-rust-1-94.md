# Rust 1.94.0 — array_windows と Cargo include

- **日付**: 2026-03-05
- **カテゴリ**: Language
- **ソース**: [Rust Blog](https://blog.rust-lang.org/2026/03/05/Rust-1.94.0/), [Phoronix](https://www.phoronix.com/news/Rust-1.94-Released), [Linuxiac](https://linuxiac.com/rust-1-94-now-available-with-new-slice-iteration-api/)

## 概要

Rust 1.94.0 は 2026年3月5日にリリースされた最新の安定版。スライスの新しいイテレーション API `array_windows` の安定化、数学定数の追加、AVX-512 FP16 intrinsics の安定化、そして Cargo の設定ファイル管理を大幅に改善する `include` キーの導入が主なハイライト。

## 主な変更点

### 言語機能

#### array_windows

スライスに `array_windows` メソッドが追加された。既存の `windows()` メソッドと同様にスライディングウィンドウを提供するが、動的サイズの `&[T]` ではなく固定サイズの `&[T; N]` を返す点が異なる。

```rust
let data = [1, 2, 3, 4, 5];
for [a, b] in data.array_windows() {
    println!("{a} + {b} = {}", a + b);
}
// 1 + 2 = 3
// 2 + 3 = 5
// 3 + 4 = 7
// 4 + 5 = 9
```

ウィンドウの長さはイテレータの使われ方から推論されるため、多くの場合明示的な指定が不要。

### 標準ライブラリ

- **数学定数の追加**: `f32` と `f64` に `EULER_GAMMA`（オイラー・マスケローニ定数）と `GOLDEN_RATIO`（黄金比）が追加
- **BinaryHeap<T>**: 一部のメソッドで `T: Ord` 制約が緩和
- **AVX-512 FP16 intrinsics** と **AArch64 NEON FP16 intrinsics** が安定化

### Cargo

#### include キー

設定ファイル（`.cargo/config.toml` 等）に `include` キーが追加され、共通設定を別ファイルに分離して読み込めるようになった。これにより、モノレポやマルチプロジェクト環境での設定管理が大幅に改善される。

```toml
include = ["../shared-config.toml"]
# optional な include も可能
include = [{ path = "../optional-config.toml", optional = true }]
```

#### TOML 1.1 サポート

マニフェスト（`Cargo.toml`）と設定ファイルで TOML 1.1 がサポートされるようになった。

### プラットフォームサポート

- RISC-V ターゲットフィーチャー29件が安定化（RVA22U64 / RVA23U64 プロファイルの大部分をカバー）

## 今後の注目点

- Rust 1.95.0 Beta が 2026年4月16日リリース予定
- Rust 1.96.0 Nightly が 2026年5月28日リリース予定
- Rust Edition 2024 の安定化（1.85.0 で達成済み）により、エコシステム全体での移行が進行中
