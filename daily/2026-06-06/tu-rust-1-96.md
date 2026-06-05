# Rust — 1.96.0

- **日付**: 2026-05-28
- **カテゴリ**: Language
- **ソース**: [Rust Blog: Announcing Rust 1.96.0](https://blog.rust-lang.org/2026/05/28/Rust-1.96.0/), [Rust Changelogs 1.96.0](https://releases.rs/docs/1.96.0/)

## 概要

Rust 1.96.0 は、言語の長年のエルゴノミクス課題のひとつである「Range 型が `Copy` でない」問題に決着をつけたリリース。`core::range` 配下に新しい Range 型を安定化し、パターンマッチ診断を強化する `assert_matches!` マクロ、WebAssembly ターゲットのリンカ挙動変更、Cargo の脆弱性修正を含む。

破壊的とまでは言えないが、WASM ターゲットのリンカ挙動変更は「これまで黙って通っていたもの」をハードエラーにするため、WASM ビルドを行うプロジェクトは要注意。

## 主な変更点

### 1. 新しい Range 型（RFC 3550）

`core::range` に新しい `Range` / `RangeFrom` / `RangeInclusive` が安定化された。従来の `std::ops::Range` は `Iterator` を直接実装していたため `Copy` にできなかったが、新型は `IntoIterator` を実装することで `Copy` を満たす。

```rust
use core::range::Range;

#[derive(Clone, Copy)]
pub struct Span(Range<usize>);

impl Span {
    pub fn of(self, s: &str) -> &str {
        &s[self.0]
    }
}
```

`Copy` 可能になったことで、構造体フィールドとして Range を保持しつつその構造体自体を `Copy` にできる、ループ後も同じ範囲を再利用できる、といったコードが書きやすくなる。

### 2. assert_matches! / debug_assert_matches! の安定化

値が指定パターンにマッチするか検証し、失敗時に `Debug` 表現付きで panic するマクロ。`assert!(matches!(..))` と機能は同等だが、失敗時の診断情報が充実している。サードパーティ crate との衝突を避けるため明示的な import が必要。

```rust
use core::assert_matches::assert_matches;

assert_matches!(get_random_number(), 1..=6);
```

### 3. WebAssembly リンカの挙動変更

全 WebAssembly ターゲットで暗黙的に付与されていた `--allow-undefined` リンカフラグが削除された。1.96 以前は未定義シンボルが自動的に `env` モジュールからの WebAssembly import に変換されていたが、今後はリンクエラーになる。

従来の挙動が必要な場合は以下で明示的に戻せる。

```bash
RUSTFLAGS="-Clink-arg=--allow-undefined" cargo build --target wasm32-unknown-unknown
```

### 4. Cargo セキュリティ修正

サードパーティレジストリ利用者向けに2件の脆弱性を修正。**crates.io 利用者は影響を受けない**。

- **CVE-2026-5223**（中度）: crate tarball 展開時のシンボリックリンク処理
- **CVE-2026-5222**（低度）: 正規化 URL での認証処理

## 破壊的変更・移行ガイド

- **WASM ビルド**: 未定義シンボルがリンクエラーになるため、ビルドが通らなくなった場合はシンボルの解決漏れを確認する。意図的に未定義 import を使っている場合のみ `-Clink-arg=--allow-undefined` を付与する。
- **新 Range 型**: 既存の `std::ops::Range` はそのまま利用可能で互換性は維持される。新型はオプトインで `core::range` から import して使う。

## 今後の注目点

- 新 Range 型がエコシステム（イテレータ系 crate、構文糖の対応）にどう波及するか。将来的に `for` ループの構文糖が新型ベースに移行する可能性がある。
- サードパーティレジストリを運用しているチームは Cargo の脆弱性対応のため早期アップグレードが推奨される。
