# Rust 1.95 — `if let` ガードと `cfg_select!` の安定化

- **日付**: 2026-04-16 リリース（記録: 2026-05-08）
- **カテゴリ**: Language（プログラミング言語）
- **ソース**: [Rust Blog 1.95.0](https://blog.rust-lang.org/2026/04/16/Rust-1.95.0/), [Rust Versions](https://releases.rs/), [LWN](https://lwn.net/Articles/1068011/)

## 概要

Rust 1.95.0 は match 式における `if let` ガードを安定化した、言語機能としての存在感が大きいリリース。長年 nightly でしか使えなかった「パターンマッチ + ガード節での再パターンマッチ」が stable で書けるようになり、ネストした列挙型やパース処理での記述量が削減できる。

合わせて、条件付きコンパイル分岐をマクロとして書ける `cfg_select!` が標準ライブラリへ取り込まれ、外部クレートの `cfg-if` を依存に持ち込まずに済むようになった。Cargo は TOML v1.1 をマニフェストおよび設定ファイルでサポート。stable コンパイラから「カスタムターゲット仕様（custom target spec）」の受け付けが取り除かれた点だけは互換性に注意が必要だが、stable のみで開発しているユーザーには影響しない。

## 主な変更点

### `if let` ガードの安定化

match arm のガード節で `if let` を使えるようになった。これまでは追加の `match` を入れ子にする必要があったケースが、ガード節で完結する。

```rust
fn classify(input: &str) -> &'static str {
    match input.parse::<i32>() {
        Ok(n) if let Some(label) = lookup(n) => label,
        Ok(n) if n.is_negative() => "negative",
        Ok(_) => "non-negative",
        Err(_) => "not a number",
    }
}
```

ガード節で得た束縛をその arm の body から参照できるため、パーサや AST の変換、トークン分類で記述量が減る。

### `cfg_select!` マクロ

外部クレート `cfg-if` 相当の機能が標準ライブラリ入り。プラットフォームごとに分岐するコードを宣言的に書ける。

```rust
let backend = cfg_select! {
    target_os = "linux" => "epoll",
    target_os = "macos" => "kqueue",
    target_os = "windows" => "iocp",
    _ => "select",
};
```

依存関係を 1 つ減らせるため、コアライブラリや組込み向けで効果が大きい。

### Cargo の TOML v1.1 サポート

`Cargo.toml` および設定ファイルが TOML v1.1 を解釈するようになった。インラインテーブルでの末尾カンマ許容など、表現の柔軟性が増す。

### 標準ライブラリ API 安定化

複数の API が stable に。リリースノートに細目が列挙されているので、自プロジェクトで該当する nightly フィーチャーフラグを使っていた場合は flag を外せる可能性がある。

## 破壊的変更・移行ガイド

- **stable での custom target spec が削除**: `--target` に JSON 形式のカスタムターゲット仕様を渡す機能は stable から外れた。標準のビルトインターゲットや、nightly + `-Z build-std` を使うケースに影響がないなら無視してよい。組込み・OS 開発で独自ターゲットを使う場合は引き続き nightly が必要。

## 今後の注目点

- 1.95 系の次は 1.96.0 の Beta が 2026-05-28 にリリース予定（[releases.rs](https://releases.rs/)）。
- `if let` ガードは過去最も望まれていた言語機能の 1 つで、ライブラリやフレームワークの API デザインに影響が出る可能性がある（特にパーサジェネレータ・状態機械の表現）。
- `cfg_select!` の登場で、`cfg-if` 依存を抜く PR が各種ライブラリで増えると見込まれる。
