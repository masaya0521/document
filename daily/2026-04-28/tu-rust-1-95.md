# Rust 1.95.0 — `cfg_select!` 安定化と let chains 由来の if-let ガード

- **日付**: 2026-04-28
- **カテゴリ**: Language（Rust）
- **ソース**: [Announcing Rust 1.95.0 — Rust Blog](https://blog.rust-lang.org/2026/04/16/Rust-1.95.0/) / [The Rust Release Announcements](https://blog.rust-lang.org/releases/)

## 概要

Rust 1.95.0 が 2026-04-16 に stable リリースされた。目玉は標準ライブラリに昇格した `cfg_select!` マクロ。これまで `cfg-if` クレートで実現していた "コンパイル時 cfg の分岐" を、外部依存なしに表現できる。加えて 1.88 で導入された let chains の延長として、`match` アームのガードに `if let` を書けるようになった。標準ライブラリでは `Vec`／`VecDeque`／`LinkedList` に "値ではなく挿入後の `&mut` を返す" 系メソッド（`push_mut` 等）が増え、`Atomic*` 型に CAS ループを抽象化する `update` / `try_update` が追加された。破壊的変更は限定的で、stable で JSON ターゲット仕様を読み込む経路が削除された。

## 主な変更点

### `cfg_select!` の安定化

`cfg` 属性をスイッチのように評価するマクロ。これまで `cfg-if` で書いていたパターンを標準で書ける。

```rust
cfg_select! {
    unix => {
        fn foo() { /* unix 固有実装 */ }
    }
    target_pointer_width = "32" => {
        fn foo() { /* 32-bit 向け */ }
    }
    _ => {
        fn foo() { /* フォールバック */ }
    }
}
```

依存削減・可読性向上に寄与し、特に新規プロジェクトでは `cfg-if` を採用しない判断が現実的になる。

### `match` ガードでの `if let`

1.88 で stable 化された let chains の応用。アームのガード式にパターンマッチを書ける。

```rust
match value {
    Some(x) if let Ok(y) = compute(x) => {
        println!("{}, {}", x, y);
    }
    _ => {}
}
```

ネストしたパターンマッチを 1 アームに統合でき、戻り値型を持つ前処理を分岐条件として組み込める。

### コレクションの `*_mut` 系 API

挿入と同時に挿入後の `&mut T` を取得できる。

- `Vec::push_mut` / `Vec::insert_mut`
- `VecDeque::push_front_mut` / `push_back_mut` / `insert_mut`
- `LinkedList::push_front_mut` / `push_back_mut`

`vec.push(x); vec.last_mut().unwrap()` のような 2 ステップが 1 ステップになり、`unwrap()` を省略できる。

### Atomic 型の `update` / `try_update`

`AtomicPtr` / `AtomicBool` / `AtomicIsize` / `AtomicUsize` に追加。CAS ループを内部に閉じ込めるユーティリティで、典型的な `compare_exchange_weak` ループのボイラープレートが減る。

### その他 stabilize された API（抜粋）

- `MaybeUninit<[T; N]>` の `From` / `AsRef` / `AsMut` 実装
- `Cell<[T; N]>` の `AsRef` 実装
- `Layout::dangling_ptr` / `repeat` / `repeat_packed` / `extend_packed`
- `bool::TryFrom<{integer}>`
- ポインタの `as_ref_unchecked` / `as_mut_unchecked`
- `core::hint::cold_path`
- const コンテキストでの `fmt::from_fn`、`ControlFlow` の各種メソッド

## 破壊的変更・移行ガイド

- **stable で JSON ターゲット仕様の読み込み経路が削除**: カスタムターゲット JSON を stable チャネルで指定する経路が消える。完全な stable ツールチェーンのみを使うユーザーには影響なし。組込／ベアメタル向けで JSON ターゲットを使う場合は nightly が必要になるケースに注意。

`cfg_select!` 自体は新規 API のため既存コードへの影響はないが、`cfg-if` を依存に持つクレートでは依存削減のリファクタが選択肢に入る。

## 今後の注目点

- **`cfg-if` 互換性の周辺整備**: `cfg-if` の API カバレッジを完全に置換できるかは個別ケースに依存する。標準ライブラリ提供のため `no_std` 環境でも追加依存なしに使える点が大きい
- **Atomic `update` / `try_update` の adoption**: ロックフリー実装でのボイラープレート削減効果。既存の `compare_exchange_weak` ループの段階的置換が進む見込み
- **Edition 2024 への波及**: 1.85 で Rust 2024 Edition が解禁されてから 1 年経過。今後の minor リリースは Edition 2024 の機能群を前提とした API 設計が増える可能性
- **次回リリース**: 6 週間サイクルで Rust 1.96 が 2026-05-28 頃に予定される。stabilize 候補は [releases.rs](https://releases.rs/) で先行確認可能
