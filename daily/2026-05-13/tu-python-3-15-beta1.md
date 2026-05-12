# Python 3.15 beta 1 — フィーチャーフリーズと 4 つの大きな変化

- **日付**: 2026-05-13
- **カテゴリ**: Language
- **ソース**: [Python Insider (Beta 1)](https://blog.python.org/2026/05/python-3150-beta-1/), [The Register](https://www.theregister.com/devops/2026/05/11/feature-freeze-for-python-315-as-first-beta-released/), [What's new in Python 3.15](https://docs.python.org/3.15/whatsnew/3.15.html), [PEP 790](https://peps.python.org/pep-0790/), [PEP 810 (Lazy imports)](https://peps.python.org/pep-0810/)

## 概要

Python 3.15 の beta 1 が 2026-05-07 にリリースされた。これはフィーチャーフリーズのタイミングで、ここからは新機能の追加は行われず、バグ修正のみで RC・正式版（2026-10-01 予定）に向かう。3.15 は「起動高速化」「マルチコア活用」「JIT 改善」「プロファイリング刷新」の 4 軸で実用フェーズに踏み込んだバージョンで、3.13 から続く CPython 並行・性能戦略の中核を担う。

最大の目玉は **PEP 810 の明示的 lazy imports**、そして **free-threaded CPython の安定 ABI (abi3t)**。前者は import 文の評価を実際に名前が使われるまで遅延させ、CLI ツールや大規模アプリの cold start を実用レベルで縮める。後者は GIL なしビルドに対する C 拡張のバイナリ互換戦略がようやく整った、というシグナルになる。

## 主な変更点

### PEP 810: 明示的 lazy imports

新しい `lazy` キーワードで import を遅延化できる。

```python
lazy import json
lazy from pathlib import Path
```

- 対象モジュールは実際に名前が参照された瞬間に初めてロードされる
- `from foo import bar` 形式でも書ける
- `__lazy_modules__` などのフックではなく、構文として明示する設計
- CLI ツールの起動時間 / サーバの cold start に効きやすい
- 既存の `_lazy_imports` 系のサードパーティ実装と違い、循環 import に強い設計

### Free-threaded Python の安定 ABI (`abi3t`)

GIL 抜きビルド向けに `t` サフィックスの安定 ABI が追加された。これにより：

- 3.15 でビルドした wheel が今後のマイナーバージョン (3.16, 3.17, ...) の free-threaded build でもそのまま動く
- ただし使える API は通常の `abi3` よりサブセット
- 拡張モジュール作者が free-threaded 環境への配布戦略を立てやすくなった

### JIT コンパイラの改善

- x86-64 Linux で平均 +8〜9% のスループット
- Apple Silicon macOS で +12〜13%
- 一方で一部コードは最大 15% 程度遅くなるケースもあるため、本番投入時はベンチ必須
- まだ「常時 ON が前提」のフェーズではないが、CPython インタプリタ単体より速いラインに乗ってきた

### サンプリングプロファイラ

- ゼロオーバーヘッドのサンプリングプロファイラが標準ライブラリ入り
- 既存の `cProfile`（instrumenting）と違い、本番に近い負荷で計測できる
- フレームグラフ生成用のデータがそのまま出せる方向

### その他

- 標準ライブラリ側で `frozendict` 相当のサポート強化
- 文字列エンコーディングのデフォルト UTF-8 化方針の継続
- 型システム周辺で `TypeIs`、`ReadOnly`、`Self` などの周辺改善

## 破壊的変更・移行ガイド

3.15 自体は大規模な破壊的変更を伴うリリースではないが、いくつか注意点がある。

- **lazy import の副作用**: モジュールトップレベルで副作用に依存しているコード（モジュール import 時に何かを登録する、import エラーを早期に表面化させたい、など）では lazy 化してはいけない。あくまでオプトイン。
- **JIT の挙動差**: ホットパスでベンチを取ること。「素の Python では速くなったがネイティブ拡張呼び出しが多いコードでは遅くなる」というケースが出る可能性がある。
- **free-threaded build 用 wheel**: `abi3t` で配るかどうかの判断が必要。CPU バウンドで GIL の影響が大きいライブラリは積極対応する価値あり。

## 今後の注目点

- 2026-10-01 の 3.15.0 正式版に向けて beta 2〜4、RC1/RC2 と継続
- lazy imports が標準ライブラリ・主要 OSS で実際にどの程度採用されるか（互換性懸念で広がりにくい歴史がある領域）
- free-threaded build が「実験的」から「サポート対象」に近づくか
- 3.13 で導入された JIT が 3.15 で実用ラインに到達するか、それともまだ 3.16 待ちか
