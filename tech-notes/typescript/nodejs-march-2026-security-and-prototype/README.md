# Node.js 2026年3月セキュリティリリース要約 & JavaScript プロトタイプ解説

## Node.js 2026年3月セキュリティリリース

2026年3月24日、Node.js は 20.x / 22.x / 24.x / 25.x の全アクティブラインに対するセキュリティアップデートを公開した。合計9件の脆弱性が修正されている。

- ソース: https://nodejs.org/en/blog/vulnerability/march-2026-security-releases

### 高危険度 (High) — 2件

| CVE | 概要 | 影響バージョン |
|---|---|---|
| CVE-2026-21637 | `loadSNI()` の不完全な修正。TLS の SNICallback が同期的な例外を適切に処理できず、プロセスクラッシュを引き起こす | 20.x, 22.x, 24.x, 25.x |
| CVE-2026-21710 | `__proto__` ヘッダー経由の DoS。HTTP リクエストに `__proto__` ヘッダーを含めると `req.headersDistinct` アクセス時に TypeError が発生しクラッシュ | 20.x, 22.x, 24.x, 25.x |

### 中危険度 (Medium) — 5件

| CVE | 概要 | 影響バージョン |
|---|---|---|
| CVE-2026-21711 | Unix ドメインソケットで Permission Model の検証がバイパスされる | 25.x のみ |
| CVE-2026-21712 | 国際化ドメイン名(IDN)の不正形式 URL 処理でアサーションエラーが発生 | 24.x, 25.x |
| CVE-2026-21713 | HMAC 検証でタイミングサイドチャネル攻撃が可能（非定時間比較による MAC 値漏洩） | 20.x, 22.x, 24.x, 25.x |
| CVE-2026-21714 | HTTP/2 の WINDOW_UPDATE フレーム処理でセッションオブジェクトのクリーンアップが失敗しメモリリーク | 20.x, 22.x, 24.x, 25.x |
| CVE-2026-21717 | V8 の文字列ハッシング機構の欠陥による HashDoS（性能低下攻撃） | 20.x, 22.x, 24.x, 25.x |

### 低危険度 (Low) — 2件

| CVE | 概要 | 影響バージョン |
|---|---|---|
| CVE-2026-21715 | `fs.realpathSync.native()` で Permission Model の権限チェックが欠落 | 20.x, 22.x, 24.x, 25.x |
| CVE-2026-21716 | Promise API の `FileHandle.chmod()` / `chown()` で権限検証が不足 | 20.x, 22.x, 24.x, 25.x |

### 対応のポイント

- 高危険度の2件（DoS系）は全バージョンに影響するため、早急なアップデートが推奨される
- 特に CVE-2026-21710 は HTTP ヘッダーに `__proto__` を送るだけでクラッシュさせられるため、外部公開サーバーは優先度高
- Permission Model 関連の修正（CVE-2026-21711, 21715, 21716）は、Permission Model を有効にしている環境で影響がある

---

## JavaScript プロトタイプ解説

CVE-2026-21710 の `__proto__` 脆弱性を理解するための背景知識。

### プロトタイプとは

プロトタイプは、オブジェクト間で機能を共有するための**仕組みの名前**である。特定のオブジェクトを指す言葉ではない。

JavaScript では、あるオブジェクトにプロパティやメソッドが見つからないとき、その**プロトタイプ（親）**を辿って探しに行く。

```javascript
const animal = {
  eat() { console.log("食べる"); }
};

const dog = Object.create(animal); // animal をプロトタイプとして dog を作成
dog.bark = function() { console.log("ワン"); };

dog.bark(); // "ワン"  ← dog 自身のメソッド
dog.eat();  // "食べる" ← dog にはないので、プロトタイプ(animal)から見つける
```

### プロトタイプチェーン

「親を辿る」動作は連鎖する。

```
dog → animal → Object.prototype → null
```

`dog.toString()` を呼ぶと：
1. `dog` にない → `animal` を見る
2. `animal` にもない → `Object.prototype` を見る
3. `Object.prototype.toString` が見つかる → 実行

`Object.prototype` が特別なのは、仕組み上ほぼ全てのチェーンの末端に位置するからであって、プロトタイプという概念そのものとは別の話である。

### class 構文との関係

ES2015 の `class` 構文は、プロトタイプの仕組みを内部で使っている。

```javascript
class Animal {
  eat() { console.log("食べる"); }
}

class Dog extends Animal {
  bark() { console.log("ワン"); }
}

const d = new Dog();
d.bark(); // "ワン"
d.eat();  // "食べる" ← プロトタイプチェーン経由
```

`class` は見た目が違うだけで、内部的にはプロトタイプチェーンで継承を実現している。

### 他の言語との比較

| 言語 | 継承の仕組み |
|---|---|
| Java / C# | クラスベース（クラスという設計図からインスタンスを作る） |
| JavaScript | プロトタイプベース（既存のオブジェクトを複製・拡張する） |

Java では「設計図（クラス）→ 実体」だが、JavaScript では「実体 → 実体」で直接つながるのが特徴。

### `__proto__` が危険な理由（プロトタイプ汚染）

`__proto__` はプロトタイプチェーンへの直接アクセス手段である。外部入力から操作できてしまうと、全く関係ないオブジェクトの振る舞いまで書き換えられてしまう。これを**プロトタイプ汚染 (Prototype Pollution)** と呼ぶ。

`__proto__`、`constructor`、`prototype` といったキーを外部入力から受け入れると、オブジェクトの継承構造が意図せず書き換わる。

対策：
- `Object.create(null)` でプロトタイプを持たないオブジェクトを使う
- 入力キーのバリデーションで `__proto__` 等を除外する
- `Map` を使う（プロトタイプチェーンの影響を受けない）
