# Rust 1.94.0 — array_windows と AVX-512 FP16

- **日付**: 2026-03-07
- **カテゴリ**: Language
- **ソース**: [Rust Blog](https://blog.rust-lang.org/2026/03/05/Rust-1.94.0/), [GitHub Release](https://github.com/rust-lang/rust/releases/tag/1.94.0), [Phoronix](https://www.phoronix.com/news/Rust-1.94-Released)

## 概要

Rust 1.94.0 が 2026年3月5日にリリースされた。主なハイライトは、スライスに対する定数長ウィンドウイテレーション `array_windows` の安定化、x86 AVX-512 FP16 および AArch64 NEON FP16 intrinsics の安定化、Cargo 設定ファイルの `include` 機能、TOML v1.1 パース対応である。

## 主な変更点

### array_windows

スライスの新しいイテレーションメソッド `array_windows` が安定化された。従来の `windows()` メソッドと異なり、定数長 `N` のウィンドウを返すため、イテレータの各要素が `&[T; N]` 型となる。これにより、パターンマッチでの分解が直接可能になり、ランタイムの境界チェックも最適化されやすくなる。

```rust
fn has_abba(s: &str) -> bool {
    s.as_bytes()
        .array_windows()
        .any(|[a1, b1, b2, a2]| (a1 != b1) && (a1 == a2) && (b1 == b2))
}
```

### AVX-512 FP16 / AArch64 NEON FP16 intrinsics

x86 の AVX-512 FP16 intrinsics と AArch64 の NEON FP16 intrinsics が安定化された。ただし、不安定な `f16` データ型に依存する intrinsics はまだ安定化されていない。AVX-512 FP16 は Intel Xeon Scalable（Sapphire Rapids 以降）でサポートされ、AMD は今後の Zen 6 プロセッサでサポート予定。

### Cargo 設定ファイルの include

`.cargo/config.toml` で `include` キーがサポートされ、複数の設定ファイルを組織的に管理・共有できるようになった。パスにはオプション指定も可能。

```toml
# .cargo/config.toml
include = ["shared-config.toml"]
include = [{ path = "optional-config.toml", optional = true }]
```

### TOML v1.1 対応

Cargo のマニフェストと設定ファイルが TOML v1.1 をパースできるようになった。これにより以下が利用可能：

- 複数行のインラインテーブル
- 新しいエスケープ文字（`\xHH`、`\e`）
- オプショナルな秒指定

## 安定化された API（17件）

- `<[T]>::array_windows`
- `<[T]>::element_offset`
- `LazyCell::get`, `LazyCell::get_mut`, `LazyCell::force_mut`
- `LazyLock::get`, `LazyLock::get_mut`, `LazyLock::force_mut`
- `impl TryFrom<char> for usize`
- `Peekable::next_if_map`, `Peekable::next_if_map_mut`
- `EULER_GAMMA`, `GOLDEN_RATIO` 定数
- x86 AVX512FP16 intrinsics
- AArch64 NEON FP16 intrinsics
- const 文脈: `f32::mul_add`, `f64::mul_add`

## 今後の注目点

- 次のベータ版 1.95.0 は 2026年4月16日予定
- ナイトリー版 1.96.0 は 2026年5月28日予定
- `f16` データ型の安定化が進めば、残りの FP16 intrinsics も利用可能になる見込み
