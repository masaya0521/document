# Rust 1.94.0 — array_windows、AVX-512 FP16、Cargo TOML 1.1

- **日付**: 2026-03-05
- **カテゴリ**: Language
- **ソース**: [Rust Blog](https://blog.rust-lang.org/2026/03/05/Rust-1.94.0/)、[Phoronix](https://www.phoronix.com/news/Rust-1.94-Released)

## 概要

Rust 1.94.0 は 2026 年 3 月 5 日にリリースされた。目玉機能はスライスの固定長ウィンドウイテレーション `array_windows`、x86 AVX-512 FP16 および AArch64 NEON FP16 イントリンシックの安定化、そして Cargo の TOML 1.1 対応と設定ファイルの `include` 機能。標準ライブラリには `EULER_GAMMA` や `GOLDEN_RATIO` などの数学定数も追加された。

## 主な変更点

### array_windows

スライスを固定長の配列ウィンドウで反復処理する新メソッド。従来の `windows()` が動的サイズの `&[T]` を返すのに対し、`array_windows()` は `&[T; N]` を返すため、パターンマッチで直接分解できる。

```rust
fn has_abba(s: &str) -> bool {
    s.as_bytes()
        .array_windows()
        .any(|[a1, b1, b2, a2]| (a1 != b1) && (a1 == a2) && (b1 == b2))
}
```

ウィンドウ長 `N` はパターンから自動推論されるため、明示的な指定が不要。

### AVX-512 FP16 / NEON FP16 イントリンシック安定化

- **x86**: AVX-512 FP16 イントリンシックが安定化。Intel Sapphire Rapids 以降のサーバー CPU でサポートされ、AMD Zen 6 でも対応予定
- **AArch64**: NEON FP16 イントリンシックが安定化

HPC や ML 推論など、半精度浮動小数点演算を活用するワークロードでのパフォーマンス向上が期待される。

### Cargo の改善

#### 設定ファイルの include 機能

`.cargo/config.toml` で他の設定ファイルを読み込めるようになった。チーム共通設定と個人設定の分離、CI 環境固有の設定管理が容易に。

```toml
include = [
    { path = "required.toml" },
    { path = "optional.toml", optional = true },
]
```

`optional = true` を指定するとファイルが存在しない場合でもエラーにならない。

#### TOML 1.1 対応

マニフェスト (`Cargo.toml`) と設定ファイルで TOML 1.1 がサポートされた。複数行のインラインテーブルと末尾カンマが使えるようになり、可読性が向上。

### 標準ライブラリの追加

- `[T]::array_windows` / `[T]::element_offset`
- `LazyCell` / `LazyLock` の `get`、`get_mut`、`force_mut` メソッド
- `char` から `usize` への `TryFrom` 実装
- 数学定数: `f32::EULER_GAMMA`、`f64::EULER_GAMMA`、`f32::GOLDEN_RATIO`、`f64::GOLDEN_RATIO`
- `f32::mul_add` / `f64::mul_add` の const 対応

## 今後の注目点

- **Rust 1.95.0**: 2026 年 4 月 16 日に Beta リリース予定
- **Rust Edition 2027**: 次の Edition に向けた議論が進行中
- AVX-512 FP16 の安定化により、Rust での ML 推論ワークロードの採用がさらに加速する可能性
