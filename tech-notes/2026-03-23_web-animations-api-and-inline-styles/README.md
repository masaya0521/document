# Web Animations API とインラインスタイルの関係

## 概要

Web Animations API（`element.animate()`）は CSS のスタイルシステムとは別のレイヤーでアニメーションを管理する。`element.style` には値が書き込まれず、独立した Animation Effects レイヤーで処理される点が最大の特徴。

## スタイルの優先順位（カスケード）

ブラウザがスタイルを解決する際の優先順位（低い順）:

1. CSS Transitions
2. CSS Animations（`@keyframes`）
3. Web Animations API（`element.animate()`）
4. inline style（`element.style.xxx`）

つまり、inline style は Web Animations API よりも優先される。

## element.style には反映されない

`element.animate()` で適用されるスタイルは inline style には書き込まれない。

```js
const el = document.querySelector('.box');
el.animate([{ opacity: 0 }], { duration: 500 });

console.log(el.style.opacity);            // "" （空文字 — 変化しない）
console.log(getComputedStyle(el).opacity); // アニメーション中の補間された値が返る
```

アニメーションは「Animation Effects」という独立したレイヤーで処理されるため、DOM の `style` 属性には一切影響しない。

## fill モードとスタイルの競合

### fill: 'forwards' の落とし穴

```js
element.animate(
  [{ transform: 'translateX(100px)' }],
  { duration: 300, fill: 'forwards' }
);
```

`fill: 'forwards'` はアニメーション終了後も最終フレームの値を Web Animations API レイヤーに保持し続ける。これにより:

- `element.style.transform = 'translateX(0)'` → inline style が勝つので**上書きできる**
- CSS クラスで `transform` を変更 → アニメーションの方が優先度が高いので**効かない**

```js
// fill: 'forwards' のアニメーションが残っている場合
element.classList.add('reset'); // CSS の transform は効かない
element.style.transform = 'translateX(0)'; // これは効く（inline style > animations）
```

### 推奨パターン: commitStyles + cancel

```js
const animation = element.animate(
  [{ opacity: 0 }, { opacity: 1 }],
  { duration: 300 }
);

animation.finished.then(() => {
  animation.commitStyles(); // 最終値を inline style に書き込む
  animation.cancel();       // アニメーションレイヤーをクリア
});
```

`commitStyles()` は最終フレームの値を `element.style` に転写する。これにより:

- アニメーションレイヤーに残骸が残らない
- 以降は通常の CSS カスケードでスタイルが管理される

`fill: 'forwards'` よりもこのパターンの方が予測可能で安全。

## 複数アニメーションの合成（composite）

```js
// 2つのアニメーションを同時に適用
element.animate(
  [{ transform: 'translateX(100px)' }],
  { duration: 500, composite: 'replace' } // デフォルト: 置き換え
);

element.animate(
  [{ transform: 'rotate(45deg)' }],
  { duration: 500, composite: 'add' } // 加算: 両方適用される
);
```

| composite    | 動作                                 |
|-------------|--------------------------------------|
| `replace`   | 既存の値を完全に上書き（デフォルト）        |
| `add`       | 既存の値に加算                         |
| `accumulate`| 数値を累積加算                         |

`replace` の場合、後から適用されたアニメーションが前のアニメーションの同じプロパティを上書きする。

## React / フレームワークとの相性

React は仮想 DOM で `style` プロパティを管理するため、`element.animate()` で変更された値は React が認識しない。

```tsx
const handleHide = (e: React.MouseEvent<HTMLDivElement>) => {
  e.currentTarget.animate(
    [{ opacity: 0 }],
    { duration: 300, fill: 'forwards' }
  );
  // React の state と DOM の実態がズレる
};
```

React と併用する場合は、アニメーション完了後に state を更新して DOM との整合性を保つ必要がある。

```tsx
const ref = useRef<HTMLDivElement>(null);

const handleHide = () => {
  const animation = ref.current?.animate(
    [{ opacity: 0 }],
    { duration: 300 }
  );

  animation?.finished.then(() => {
    setVisible(false); // アニメーション完了後に state を同期
  });
};
```

## getComputedStyle との関係

```js
// アニメーション中の現在値を取得できる
const current = getComputedStyle(element).opacity;
// → アニメーション中の補間された値が返る
```

`getComputedStyle` はアニメーションレイヤーを含む最終的な計算値を返すため、アニメーション中の値を正確に取得できる。

## まとめ

| 項目                    | 説明                                                        |
|------------------------|-------------------------------------------------------------|
| inline style への影響    | `animate()` は `element.style` を変更しない                    |
| 優先順位                | inline style > Web Animations API > CSS Animations > Transitions |
| 終了後の保持             | `fill: 'forwards'` で保持可能だが `commitStyles()` + `cancel()` が推奨 |
| フレームワーク連携        | 状態管理と乖離しやすいので、完了後の state 同期が必要              |
| getComputedStyle        | アニメーション中の補間値を含む最終計算値を返す                      |

## 参考

- [MDN - Web Animations API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API)
- [MDN - Element.animate()](https://developer.mozilla.org/en-US/docs/Web/API/Element/animate)
- [MDN - Animation.commitStyles()](https://developer.mozilla.org/en-US/docs/Web/API/Animation/commitStyles)
