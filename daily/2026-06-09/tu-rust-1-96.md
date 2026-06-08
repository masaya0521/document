# Rust 1.96.0 — 新レンジ型の安定化と assert_matches!

- **日付**: 2026-06-09
- **カテゴリ**: Language
- **ソース**: [Announcing Rust 1.96.0](https://blog.rust-lang.org/2026/05/28/Rust-1.96.0/), [1.96.0 Changelog](https://releases.rs/docs/1.96.0/)

## 概要

Rust チームは 2026年5月28日、Rust 1.96.0 を安定版としてリリースした（master からの分岐は 4月10日）。本リリースの目玉は **RFC3550 由来の新レンジ型の安定化** で、長年の課題だった「`Range` が `Iterator` であるがゆえに `Copy` を実装できない」問題に対する解決策が `core::range` 名前付きモジュールとして提供される。あわせてパターンマッチ診断用の `assert_matches!` マクロ、WebAssembly リンク時の挙動変更などが含まれる。

また、crate tarball の展開と URL 正規化に関するセキュリティ脆弱性（CVE-2026-5222 / CVE-2026-5223）も修正されている。主に影響を受けるのはサードパーティレジストリの利用者であり、crates.io 利用者への直接影響は限定的とされる。

## 主な変更点

### 新レンジ型の安定化（RFC3550）

- `core::range::Range` / `RangeFrom` / `RangeInclusive` が安定化。
- 従来の `std::ops::Range` は `Iterator` を実装しているため `Copy` にできなかったが、新型はイテレータと値を分離する設計により、`Copy` でより扱いやすいレンジ表現を提供する。
- スライス操作などでレンジを複数回使い回すケースで `.clone()` が不要になり、安全性と取り回しが向上する。

### assert_matches! マクロ

- `assert_matches!` と `debug_assert_matches!` を追加。値が指定パターンにマッチするかをアサートし、失敗時に分かりやすい診断を出力。
- サードパーティ crate との衝突を避けるため、手動 import が必要。

```rust
use core::assert_matches::assert_matches;

let value = Some(42);
assert_matches!(value, Some(x) if x > 0);
```

### WebAssembly のリンク変更

- WebAssembly ターゲットで、リンク時に未定義シンボルをデフォルトで許可しなくなった。明示的に再有効化しない限りエラーとなる。
- 設定ミスや潜在バグを早期に検知できるようになる一方、既存の Wasm ビルドでリンクエラーが顕在化する可能性がある。

## 破壊的変更・移行ガイド

- **Wasm の未定義シンボル禁止**: これまで暗黙的に許可されていた未定義シンボルがリンクエラーになる。意図的に未定義シンボルを残す構成では、リンカフラグでの明示的な再有効化が必要。
- `assert_matches!` は prelude に含まれないため、利用箇所で明示的に `use` する。

## 今後の注目点

- 新レンジ型は当面 `std::ops::Range` と併存する。エコシステム（crate API のシグネチャ）がどの程度新型へ移行していくかが普及の鍵。
- CVE 修正を含むため、サードパーティレジストリ運用者は早めのアップデートが推奨される。
- 6週間サイクルのため、次の 1.97.0 は 7月上旬の安定化が見込まれる。
