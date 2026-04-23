# Rust 1.95 — `cfg_select!` と if-let ガードで pattern matching を強化

- **日付**: 2026-04-23（リリース日: 2026-04-16）
- **カテゴリ**: Language
- **ソース**: [Rust Blog (1.95.0)](https://blog.rust-lang.org/2026/04/16/Rust-1.95.0/), [Phoronix 解説](https://www.phoronix.com/news/Rust-1.95-Released), [Linuxiac 解説](https://linuxiac.com/rust-1-95-released-with-new-match-guards-and-stable-api-additions/)

## 概要

Rust 1.95.0 は 2026-04-16 にリリースされた。今回の目玉は **`cfg_select!` マクロの安定化** と **match の if-let ガード**。前者はこれまで `cfg-if` クレートで補っていた「コンパイル時の条件分岐」を標準で表現可能にし、後者は 1.88 で入った let chain を match arm にも持ち込むもの。stable API も atomic / `MaybeUninit` / `Cell` 関連を中心に拡張されている。一方で **stable toolchain での custom target spec の受け入れが廃止** され、低レイヤ・組み込み向け開発者には影響がある変更も含まれる。

## 主な変更点

### `cfg_select!` マクロ

`cfg` 述語を「コンパイル時の `match`」のように扱える組み込みマクロ。これまで定番だった `cfg_if!` クレート相当の機能が言語標準で利用できるようになった。

```rust
cfg_select! {
    unix => { fn foo() { /* unix 向け */ } }
    target_pointer_width = "32" => { fn foo() { /* 32-bit 向け */ } }
    _ => { fn foo() { /* フォールバック */ } }
}
```

依存クレートを減らせるだけでなく、`cfg(...)` 属性の入れ子で読みづらくなりがちなプラットフォーム別実装をフラットに書ける。

### match の if-let ガード

1.88 で入った let chain を match arm のガード条件にも書けるようになった。

```rust
match value {
    Some(x) if let Ok(y) = compute(x) => {
        println!("{x}, {y}");
    }
    _ => {}
}
```

これまでは内側で `match` をネストしたり `if let ... else { continue; }` のような書き方になっていたパターンを、ガード条件のまま簡潔に表現できる。

### API 安定化

- atomic 系: `update` / `try_update` 系メソッド
- メモリ周り: `MaybeUninit` ⇄ `Cell` 変換ヘルパー、unchecked なポインタ操作
- コレクション: `push_mut` / `insert_mut` 系のバリアント
- 既存 API の **const コンテキスト対応** がいくつか追加

## 破壊的変更・移行ガイド

### Stable で JSON ターゲット仕様の受け入れを廃止

`rustc` に対してカスタムターゲット仕様（JSON）を渡す機能が **stable toolchain では削除** された。

- 影響を受けるのは主に **組み込み・OS 開発・特殊ターゲット向けにクロスビルドしているユーザー**。
- 標準ライブラリのビルド自体がもともと nightly 機能を要求していたため、「純粋な stable 利用者」にはほぼ影響なし。
- 該当する場合は nightly toolchain に切り替えるか、独自ターゲットを upstream に取り込む方向で運用を見直す必要がある。

## 今後の注目点

- **Rust 1.96.0 は 2026-05-28 リリース予定**（現在 beta）。リリーストレインは順調。
- `cfg_select!` の浸透で、`cfg-if` クレート依存をやめる動きがクレート側にも広がるはず。SDK / 組み込み系ライブラリが標準マクロベースに書き換えていくかをウォッチしたい。
- if-let ガードと let chain の組み合わせで「ネストの浅い state machine」が書きやすくなった。`async`/`await` 周りのエラーハンドリングと組み合わせた書き方の流行に注目。
