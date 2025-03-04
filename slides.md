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



---
class: flex justify-center items-center

---

# 2-7 畫面組裝的藍圖：component 初探

---

# 什麼是 Component

---

# 定義 Component

```jsx
// MyButton.jsx
export default function MyButton(props) {
  return (
    <button>I'm a button</button>
  );
}
```

<br>

- class component --> function component + hooks
- Component component 名稱首字母必須大寫

---

# 呼叫 Component

````md magic-move
```jsx
const reactElement = <div id="foo" />;
```

```jsx
const reactElement = React.createElement('div', { id: 'foo' });
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

# Props

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

