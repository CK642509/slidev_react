---
theme: seriph
background: https://i.ytimg.com/vi/5CXQDCEZtPc/sddefault.jpg
title: 《React 思維進化》簡報
info: |
  ## 關於這份簡報
  嗨！我是上竣~

  這是[《React 思維進化》讀書會](https://github.com/Tech-Book-Community/Zet-React-Book)的簡報

  原始檔都放在[Github](https://github.com/CK642509/slidev_react)上，歡迎查看
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
---

# React 思維進化讀書會

## 2-7 ~ 2-9

2025.03.18

---

# 上竣
- 非本科系 (農業化學系、生醫電資所)
- ~ 3 年年資
- AI 新創公司，全端開發 (Vue + Python)
- iThome 鐵人賽
  - 2024 Python 組 「用 Python 打造你的 Discord BOT」 佳作
  - 2023 Software Development 組 「FastAPI 開發筆記：從新手到專家的成長之路」

---

# 前情提要

- DOM vs. vDOM
- React Element
- JSX
- 單向資料流 與 一律重繪

<br><br><br>

<v-click>

<div class="text-center">

## Component

</div>

</v-click>

<br>

<v-click>

<div class="text-center">

### 2-7 畫面組裝的藍圖：component 初探
### 2-8 React 畫面更新的發動機：state 初探
### 2-9 React 畫面更新的流程機制：reconciliation

</div>

</v-click>

<!-- 
- [click] 導入一個新的概念，叫做 component
- [click] 在 2-7 會簡單介紹什麼是 component，以及如何透過 props，將外部參數傳入到 component 內
- 接著，在 2-8 會介紹什麼是 state，以及在 component 內，如何用 state 做資料狀態管理與畫面更新
- 最後，在 2-9 會以 component 的角度，再完整地走過一次 React 畫面更新的流程機制 -->


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

- Input: props (properties 的意思)
- Output: React Element

<v-click>

#
- Component component 名稱首字母必須大寫
  - transpiler 在做 JSX 轉譯時，會依據首字母大小寫來判斷該怎麼呼叫 `React.createElement`
    - 字串，e.g. `React.createElement('div')`
    - 變數名稱，e.g. `React.createElement(MyButton)`

</v-click>

---

# 呼叫 Component

- 之前有介紹過，React element 可以這樣建立：

````md magic-move
```js
const reactElement = React.createElement("div", { id: "foo" });
```

```jsx
const reactElement = <div id="foo" />;
```
````
<br>

<v-click>

- React element 的類型其實也可以是自定義的 component：

````md magic-move
```js
const reactElement = React.createElement(MyButton);
```

```jsx
const reactElement = <MyButton />;
```
````

</v-click>

---

# 藍圖與實例

- Component --> 藍圖
- 呼叫 Component --> 產生實例 (instance)

<br>

<v-click>

- 珍珠奶茶製作配方 --> 藍圖
- 調製珍珠奶茶 --> 產生實例

</v-click>

<br>

<v-click>

- 珍珠奶茶 component
  - 實際做好的珍珠奶茶 ❌
  - 珍珠奶茶的製作配方 ✔️

</v-click>

<br>

<v-click>

- 重複使用珍珠奶茶 component --> 以這套製作配方去重複產出很多杯珍珠奶茶
  - 這些珍珠奶茶彼此獨立，不互相影響
  - 可以客製化去調整甜度、冰塊

</v-click>


---
layout: TwoColumn57
---

# Props

- props 是 component 藍圖的「變因」或「參數」
- 將 props 從外部傳入 component，可進行畫面產生流程的客製化，以應付更多需求情境
- props 是唯讀且不可被修改的

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
layout: TwoColumn57
---

# 特殊的 prop：children

````md magic-move
```jsx
<MyCard children="這裡的內容就是 children props 的值" />
```

```jsx
<MyCard>這裡的內容就是 children props 的值</MyCard>
```
````

<br>

<v-click>

- 可以在開標籤與閉標籤之間填寫 prop 值 --> 設計「容器與內容」相關的 component 更方便與直覺

</v-click>

::left::

<v-click>

<div class="mr-4">
```jsx
// MyComponent.jsx
export default function MyCard(props) {
  return (
    <div className="crad">
      {props.children}
    </div>
  )
}
```
</div>

</v-click>

::right::

<v-click>

```jsx
function App() {
  return (
    <MyCard>
      <h1>Hello, world!</h1>
      <p>Welcome to my website.</p>
    </MyCard>
  )
}
```

</v-click>

<v-click>

- 除了特有的傳值方式之外，本質上與其他 props 沒有什麼區別
- React 本身並沒有預設 children prop 的用途

</v-click>

---

# Component 的 render 與 re-render

---

# 2-7 重點整理

- Component
- 藍圖 vs. 實例
- props

圖



---

# Quiz

## Q1: 為什麼 component 命名中的首字母必須為大寫?


---
layout: two-cols
---

# Quiz

## Q2: 請問 console 中依序會印出什麼?
- (A) 111
- (B) 222
- \(C) 333
- (D) 444

::right::


```jsx {*}{maxHeight:'65vh'}
// index.js
import ReactDom from 'react-dom/client';

function MyComponent1(props) {
  console.log("render MyComponent1")
  return (
    <div className="MyComponent1-wrapper">
      <h1>I am MyComponent1</h1>
      <MyComponent2 />
      <MyComponent2 />
    </div>
  );
}

function MyComponent2(props) {
  console.log("render MyComponent2")
  return (
    <div className="MyComponent2-wrapper">
      <MyComponent3 />
      <MyComponent3 />
    </div>
  );
}

function MyComponent3(props) {
  console.log("render MyComponent3")
  return (
    <div className="MyComponent3-wrapper">
      <h3>I am MyComponent3</h3>
    </div>
  );
}

const root = ReactDOM.createRoot(
  document.getElementById('root')
);
root.render(<MyComponent1 />)
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
- 狀態資料
- 臨時的「可更新的資料」

<br>

### 單向資料流
- 當畫面更新時，畫面才會發生對應的更新，以資料去驅動畫面

<br>

### 一律重繪策略
- 沒必要重繪整個畫面，只需要重繪與有被更新的資料相關的區塊即可
- component 是 state 機制運作的載體，也是一律重繪的界線

<br>

> ### state 必須依附在 component 之上，發起 state 更新並啟動重繪時，只會重繪該 component 以內 (包含子孫代 component) 的畫面區塊




---

# useState 初探

- 在 function component 中，可透過 `useState` 這個 hook 來定義與存取 state

````md magic-move {lines: true}
```jsx {*|2,5,9|*}
// Counter.jsx
import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <button>-</button>
      <span>{count}</span>
      <button>+</button>
    </div>
  );
}
```

```jsx {*|7-13,17,19|5,8,12|*}
// Counter.jsx
import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  const handleDecrementButtonClick = () => {
    setCount(count - 1);
  };

  const handleIncrementButtonClick = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <button onClick={handleDecrementButtonClick}>-</button>
      <span>{count}</span>
      <button onClick={handleIncrementButtonClick}>+</button>
    </div>
  );
}
```
````

---

# 關於 state 的補充觀念 (1)

- hooks 僅可以在 component function 內的頂層作用域被呼叫 

````md magic-move {lines: true}
```jsx {*|2,3,16|2,5-7,16|2,9-11,16|2,13-15,16|2,16,18|*}
// index.js
function AppComponent() {
  useState();  // ✔️

  if (...) {
    useState();  // ❌
  }

  for (...) {
    useState();  // ❌
  }

  array.forEach(() => {
    useState();  // ❌
  })
}

useState();  // ❌
```
````

---

# 關於 state 的補充觀念 (2)

- `useState` 的回傳值是一個陣列
  - 讓開發者在呼叫 `setState` 時，可以更方便分別賦值到自訂命名的變數上

<v-click>

````md magic-move
```js {1,2|*}
// 假設是回傳物件
const { state, setState } = useState();

const { state: count, setState: setCount } = useState(0);
const { state: name, setState: setName } = useState("Foo");
```

```js
// 回傳陣列
const [state, setState] = useState();

const [count, setCount] = useState(0);
const [name, setName] = useState("Foo");
```
````

</v-click>

<br>

<v-click>

- 呼叫 `setState` 方法是更新 state 值並觸發 re-render 的唯一合法手段

</v-click>

<br>

<v-click>

- React 是依據 hooks 的固定的呼叫順序來區別彼此

</v-click>

<br>

<v-click>

- 同一個 component 的同一個 state，在該 component 的不同實例之間的狀態資料是獨立的

</v-click>


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


---

# Render phase 與 commit phase

圖

---

# Reconciliation

圖

1. 呼叫 `setState` 方法更新資料
   - 執行 `Object.is()` 檢查 state 是否有不同
2. 更新資料並 re-render component function
3. 比較新舊版本的 React element
4. 更新差異之處所對應的實際 DOM element

圖 2-9-2

---
layout: two-cols-header
---

# setState 觸發的 re-render 會連帶觸發子 component 的 re-render

- Component 共有兩種會被觸發 re-render 的可能情形
  1. 本身的 `setState`
  2. 父層 component re-render

::right::

<v-click>

![](https://mokkapps.twic.pics/mokkapps.de/blog/debug-why-react-re-renders-a-component/react-vdom-dom_hmargb.jpg)
<span class="opacity-30 text-xs">https://mokkapps.de/blog/debug-why-react-re-renders-a-component</span>

</v-click>

---

# Quiz

## Q6: 請解釋 React 更新畫面的 reconciliation 流程

<br>

## Q7: 一個 component 有哪些可能會被觸發 re-render 的情形？

---
class: flex justify-center items-center

---

# 第二章回顧

---



---
class: flex justify-center items-center

---

# Thank you