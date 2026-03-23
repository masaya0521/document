# addEventListener の capture オプション

## DOM イベントの伝播フェーズ

DOM イベントは3つのフェーズで伝播する。

1. **キャプチャフェーズ** — `window` → `document` → ... → ターゲットの親まで、上から下へ降りていく
2. **ターゲットフェーズ** — イベントが発生した要素自体
3. **バブリングフェーズ** — ターゲットの親 → ... → `document` → `window` まで、下から上へ昇っていく

```
window → document → div → button (ターゲット) → div → document → window
|______ キャプチャ ______|                    |______ バブリング ______|
```

## capture オプション

通常の `addEventListener` はバブリングフェーズでリスナーが呼ばれるが、`capture: true` を指定するとキャプチャフェーズ（上から下）で呼ばれる。

```js
// バブリングフェーズで発火（デフォルト）
element.addEventListener('click', handler);

// キャプチャフェーズで発火
element.addEventListener('click', handler, { capture: true });

// 第3引数に true を渡す省略形
element.addEventListener('click', handler, true);
```

## 用途

### 他のハンドラより先にイベントを処理したい場合

キャプチャはバブリングより先に実行されるので、子要素のハンドラより先に親で処理できる。

### stopPropagation() で止められたイベントを捕捉したい場合

子要素がバブリングを止めていても、キャプチャフェーズなら親で検知できる。

### フォーカス系イベントの委譲

`focus` や `blur` はバブルしないが、キャプチャなら親要素で受け取れる。

```js
// focus はバブルしないので、通常の委譲では検知できない
parentEl.addEventListener('focus', handler); // 子の focus は来ない

// キャプチャなら親で子の focus を検知できる
parentEl.addEventListener('focus', handler, true); // 子の focus を検知できる
```

## removeEventListener との対応

`capture: true` で登録したリスナーを削除するには、`removeEventListener` でも `capture: true` を指定する必要がある。capture の値が異なると別のリスナーとして扱われる。

```js
// 登録
element.addEventListener('click', handler, true);

// 削除（capture: true が必要）
element.removeEventListener('click', handler, true);
```
