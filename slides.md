---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Welcome to Slidev
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
---

# React 思維進化讀書會

## 2-7 ~ 2-9

2025.03.18

---

# 上竣
- 非本科系 (農業化學系、生醫電資所)
- ~ 3 年年資
- 新創，全端開發 (Vue + Python)
- iThome 鐵人賽
  - 2024 用 Python 打造你的 Discord BOT
  - 2023 FastAPI 開發筆記：從新手到專家的成長之路

---

# 前情提要

- DOM vs. vDOM
- React Element
- JSX
- 單向資料流 與 一律重繪

## Component


---
class: flex justify-center items-center

---

# 2-7 畫面組裝的藍圖：component 初探

---
layout: two-cols
---

# 什麼是 Component

<v-click>

- 由開發者自定義的畫面元件藍圖
- 可重用的程式碼片段

</v-click>

<v-click>

## 抽象化
- 根據需求，將關心的特徵與行為歸納出來
- 將實作細節或複雜性封裝在內部
- 通用性、重用性

</v-click>

::right::

<br><br><br><br><br><br>

<v-click>

![](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*wmRD7YIgQsWEt8PBa1dIyQ.png)
<span class="opacity-30 text-xs">https://sam-j.medium.com/react-component-structure-d38d59eefffd</span>

</v-click>


---

# 定義 Component


- 可透過 function 來定義，也可以用 class 定義
  - React 16.8 之後，function component + hooks 成為主流

```jsx
// MyButton.jsx
export default function MyButton(props) {
  return (
    <button>I'm a button</button>
  );
}
```

<br>

- Input: props (properties 的意思)
- Output: React Element

#
- Component component 名稱首字母必須大寫

---

# 呼叫 Component

````md magic-move
```jsx
const reactElement = <div id="foo" />;
```

```jsx
const reactElement = React.createElement("div", { id: "foo" });
```
````
<br>

<v-click>

````md magic-move
```jsx
const reactElement = <MyButton />;
```

```jsx
const reactElement = React.createElement(MyButton);
```
````

</v-click>

---

# 藍圖與實例

---
layout: TwoColumn57
---

# Props

- props 是 component 藍圖的「變因」或「參數」
- 將 props 從外部傳入 component，可進行畫面產生流程的客製化，以應付更多需求情境

::left::

<div class="mr-4">
```js
// index.js
const reactElement = (
  <div>
    <ProductListItem
      title="Apple"
      price={100}
      imageUrl="https://example.com/apple.jpg"
    />
    <ProductListItem
      title="Banana"
      price={150}
      imageUrl="https://example.com/banana.jpg"
    />
  </div>
);
```
</div>

::right::

````md magic-move
```jsx
// ProductListItem.jsx
export default function ProductListItem(props) {
  return (
    <div>
      <img src={props.imageUrl} />
      <h2>{props.title}</h2>
      <p>${props.price}</p>
    </div>
  );
}
```

```jsx
// ProductListItem.jsx
export default function ProductListItem({title, price, imageUrl}) {
  return (
    <div>
      <img src={imageUrl} />
      <h2>{title}</h2>
      <p>${price}</p>
    </div>
  );
}
```
````


---

# 特殊的 prop：children


---

# Component 的 render 與 re-render

---

# 2-7 重點整理

---

# Quiz

## Q1: 為什麼 component 命名中的首字母必須為大寫?


---

# Quiz

## Q2: 請問 console 中依序會印出什麼?
- (A) 111
- (B) 222
- \(C) 333
- (D) 444


```jsx
// MyButton.jsx
export default function MyButton(props) {
  return (
    <button>I'm a button</button>
  );
}
```

---

# Quiz

## Q3: 下列哪個才是正確的 props 正確使用方法?

```jsx
// MyButton.jsx
export default function ProductListItem(props) {
  props.price = props.price * 0.9
  return (
    <button>I'm a button</button>
  );
}
```

---
class: flex justify-center items-center

---

# 2-8 React 畫面更新的發動機：state 初探

---

# 什麼是 state?

---

# useState 初探

--- 

# 2-8 重點整理

---

# Quiz

## Q4: state 的本質是什麼? state 與 component 的關係是什麼?

<br>

## Q5: 同一個 component 在多個地方被呼叫，它們之間的 state 資料會互通嗎? 為什麼?

---
class: flex justify-center items-center

---

# 2-9 React 畫面更新的流程機制：reconciliation

