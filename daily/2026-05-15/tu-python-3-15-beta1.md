# Python 3.15.0 beta 1 — feature freeze と lazy imports / 安定 free-threaded ABI / Tachyon プロファイラ

- **日付**: 2026-05-15
- **カテゴリ**: Language
- **ソース**: [Python Insider](https://blog.python.org/2026/05/python-3150-beta-1/), [What's New in Python 3.15](https://docs.python.org/3.15/whatsnew/3.15.html), [The Register](https://www.theregister.com/devops/2026/05/11/feature-freeze-for-python-315-as-first-beta-released/), [InfoWorld](https://www.infoworld.com/article/4166693/the-best-new-features-in-python-3-15.html)

## 概要

Python 3.15.0 の最初のベータが 2026-05-11 にリリースされ、これをもって 3.15 は **feature freeze（機能凍結）** に入った。以降のリリースに向けては安定化とバグ修正のみが行われ、新機能の追加はない。正式リリースは 2026-10-01 の予定。

3.15 は CPython にとって長期的な改善が一気に実用フェーズに入る節目のリリースで、特に **(1) 起動・モジュール読み込みの軽量化を狙う lazy imports（PEP 810）**、**(2) 3.13 で導入された free-threaded ビルドの安定 ABI 化**、**(3) 大幅に強化された JIT** が三本柱になる。

## 主な変更点

### Lazy Imports（PEP 810）

大規模 Python アプリケーションの起動が遅い主因のひとつはインポートシステムで、依存ツリーが深いとファイル解決・読み込み・コンパイル・トップレベル実行のコストが数秒単位で積み上がる。3.15 は **`lazy` ソフトキーワード** によって明示的な遅延インポートを言語レベルで提供する。

```python
lazy import numpy as np
lazy from rich.console import Console

def render():
    # ここで初めて numpy / rich が実際に読み込まれる
    return Console().print(np.array([1, 2, 3]))
```

- ファイル冒頭に import を集約するという可読性の利点を保ちつつ、実際に使われるモジュールのコストしか払わない
- ソースコードを変えずに全体へ適用したい場合は、`-X lazy_imports` コマンドラインオプションまたは `PYTHON_LAZY_IMPORTS` 環境変数を使う
- 値は `all`（既定でレイジー）/ `none`（無効）/ `normal`（既定。ソース中の `lazy` キーワードを尊重）の3種

### Free-Threaded ビルドの安定 ABI（abi3t）

3.13 で実験的に導入された **GIL なし（free-threaded）ビルド** に対して、3.15 では **安定 ABI が `t` サフィックス（abi3t）** として確立される。つまり、3.15 で 1 度ビルドした free-threaded 用 C 拡張は、将来の Python バージョンでもそのまま使えるようになる。これによりエコシステム側（NumPy / Pillow など C 拡張を出荷するライブラリ）はバージョンごとに再ビルドする必要がなくなり、free-threaded Python の採用障壁が大きく下がる。

### JIT コンパイラの強化

3.15 の JIT は CPython インタプリタに対し以下の平均改善を達成:

- **x86-64 Linux**: 約 8〜9% 高速化
- **Apple Silicon macOS**: 約 12〜13% 高速化

主な技術的変化:

- 新しい **tracing front end** によるトレース生成
- **レジスタアロケーション** の導入で高速かつメモリ効率の良い実行
- JIT 生成コードの改善
- 一部オブジェクトの参照カウント省略など追加の最適化

### 新しい Tachyon サンプリングプロファイラ

オーバーヘッドのほぼゼロな **サンプリングプロファイラ（Tachyon）** が標準で搭載される。本番環境を含む長時間プロセスのプロファイリングを実用的に行えるようになる。

### その他

- UTF-8 がテキストエンコーディングのデフォルトに（プラットフォーム依存からの脱却）
- Tier 2 / Tier 3 関連の細かな改善やライブラリ更新も多数

## 破壊的変更・移行ガイド

3.15 自体は機能凍結に入った段階で 10 月の GA まで安定化期間に入る。移行で押さえるべきポイント:

- **ライブラリ作成者**: free-threaded 拡張を提供するなら abi3t での再ビルドが推奨される。今後のメジャーバージョンを跨いでバイナリ互換が保てる
- **大型アプリのオーナー**: 既存コードに `lazy` を入れる前に、`-X lazy_imports=all` で全レイジー化したときの挙動を確認するのが安全。トップレベルで副作用に依存しているコードは破綻する可能性がある
- **3.14 ユーザー**: 3.14 系で実験的に試した GC まわりは 3.13 の世代別 GC に戻されている（3.14.5 で revert 済み）ので、メモリ動作の前提が変わっている点に注意

## 今後の注目点

- 正式リリース 2026-10-01 までの間、ベータ → RC を経た最終調整
- free-threaded ビルドが「実験」から「主流選択肢」に格上げされるかは、主要 C 拡張の abi3t 対応状況次第
- lazy imports の普及度合いと、サーバレスやコンテナの cold start 改善への効果
- Tachyon を使った本番プロファイリングのプラクティスがコミュニティでどう蓄積されるか
