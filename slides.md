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

<!-- [click]作者有提到，習慣上會使用解構的方式直接在參數中提取所需的內容 -->

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

<!-- 
- 在 React 中，有一個特殊的 prop，叫做 children。
- 這是一個簡單的範例
- [click]但它也可以改成這樣寫
- [click]這樣寫的好處是
-->

---

# Component 的 render 與 re-render

<v-switch>
  <template #1>
    <img
      src="/process_all_2.svg"
      alt=""
    />
  </template>
  <template #2>
    <img
      class="ml-3 mt-7"
      src="/components_2.svg"
      alt=""
    />
  </template>
  <template #3>
    <img
      src="/components.svg"
      alt=""
    />
  </template>
</v-switch>

<!-- 
- 最後，來介紹一下 component 的 render 與 re-render
- [click]這是我自己畫的一個流程圖，解釋...
- ...稱為「一次 render」，...稱為「re-render」
- [click]當 component 第一次 render 時，它會依序去 render 它的子 component
- 以這個圖為例，component 1 有兩個子 component 叫 component 2，而 component 2 也有 2 個子 coponent
- [click]在一次 render 時就會是這個順序
-->

---

# Quiz

## Q1: 為什麼 component 命名中的首字母必須為大寫?

<br>

<v-click>

> - #### 為了滿足 JSX 語法在轉譯時的元素類型判斷需求

> - #### 也是 React 社群在開發上的命名慣例

</v-click>


---
layout: two-cols
---

# Quiz

## Q2: 請問 console 中依序會印出什麼?
- (A) 1 2 2 3 3 3 3
- (B) 1 2 3 3 2 3 3
- \(C) 1 2 3 2 3 3 3

<img
  v-click
  class="w-80"
  src="/components_2.svg"
  alt=""
/>

::right::


```jsx {*}{lines: true, maxHeight:'65%'}
// index.js
import ReactDom from 'react-dom/client';

function MyComponent1(props) {
  console.log("1")
  return (
    <div className="MyComponent1-wrapper">
      <h1>I am MyComponent1</h1>
      <MyComponent2 />
      <MyComponent2 />
    </div>
  );
}

function MyComponent2(props) {
  console.log("2")
  return (
    <div className="MyComponent2-wrapper">
      <h2>I am MyComponent2</h2>
      <MyComponent3 />
      <MyComponent3 />
    </div>
  );
}

function MyComponent3(props) {
  console.log("3")
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
layout: two-cols-header
---

# Quiz

## Q3: 下列哪個才是正確的 props 正確使用方法? 為什麼?

::left::

### (A)

<div class="mr-4">
```jsx {*|1,2,5}{lines: true}
export default function ProductListItem(props) {
  props.price = props.price * 0.9
  return (
    <div>
      <p>折扣價：{props.price}</p>
    </div>
  );
}
```
</div>

### (B)

<div class="mr-4">
```jsx {*|1,2,5}{lines: true}
export default function ProductListItem(props) {
  const discountPrice = props.price * 0.9
  return (
    <div>
      <p>折扣價：{discountPrice}</p>
    </div>
  );
}
```
</div>

::right::

### \(C)
```jsx {*|1,2,5}{lines: true}
export default function ProductListItem({ price }) {
  price = price * 0.9
  return (
    <div>
      <p>折扣價：{price}</p>
    </div>
  );
}
```

---
class: flex justify-center items-center

---

# 2-8 React 畫面更新的發動機：state 初探

---

# 狀態更新...?

<br>

<v-switch>
  <template #1>
    <img
      src="/process_all_2.svg"
      alt=""
    />
  </template>
  <template #2>
    <img
      src="/process_all_2_setState.svg"
      alt=""
    />
  </template>
</v-switch>

---

# 什麼是 state?
- 狀態資料
- 臨時的「可更新的資料」

<br>

<v-click>

### 單向資料流
- 當畫面更新時，畫面才會發生對應的更新，以資料去驅動畫面

</v-click>

<br>

<v-click>

### 一律重繪策略
- 沒必要重繪整個畫面，只需要重繪與有被更新的資料相關的區塊即可
- component 是 state 機制運作的載體，也是一律重繪的界線

</v-click>

<br>

<v-click>

> #### state 必須依附在 component 之上，發起 state 更新並啟動重繪時，只會重繪該 component 以內 (包含子孫代 component) 的畫面區塊

</v-click>

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

# Quiz

## Q4: state 的本質是什麼? state 與 component 的關係是什麼?

<br>

<v-click>

> - #### state 是前端應用程式中用於記憶狀態的臨時、可更新資料，並且在資料更新時更新對應的畫面

> - #### state 必須依附在 component 內才能記憶並維持狀態資料，而發起該 state 資料的更新並啟動重繪時，只會重繪該 component 以內 (包含子孫代 component)的畫面區塊

</v-click>

<br>

## Q5: 同一個 component 在多個地方被呼叫，它們之間的 state 資料會互通嗎? 為什麼?

<br>

<v-click>

> - #### 不會，同一個 component 的同一個 state，在該 component 的不同實例之間的狀態資料是獨立的

</v-click>


---
class: flex justify-center items-center

---

# 2-9 React 畫面更新的流程機制：reconciliation


---

# Render phase 與 commit phase

<br>

<v-switch>
  <template #1>
    <img
      src="/process_all_2.svg"
      alt=""
    />
  </template>
  <template #2>
    <img
      src="/process_all.svg"
      alt=""
    />
  </template>
  <template #3>
    <img
      src="/process_render.svg"
      alt=""
    />
  </template>
  <template #4>
    <img
      src="/process_re-render.svg"
      alt=""
    />
  </template>
</v-switch>

---
layout: two-cols-header

---

# Reconciliation


<div>
  <img
    v-click
    class="w-150"
    src="/process_re-render.svg"
    alt=""
  />
</div>

<v-click>

1. 呼叫 `setState` 方法更新資料
   - 執行 `Object.is()` 檢查 state 是否有不同
2. 更新資料並 re-render component function
3. 比較新舊版本的 React element
4. 更新差異之處所對應的實際 DOM element

</v-click>

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

<v-click>

> #### 1. 呼叫 `setState` 方法更新 state 資料，並發起 re-render
> #### 2. 更新 state 資料並 re-render component function
> #### 3. 將新舊版本的 React Element 進行結構比較，並更新差異之處所對應的實際 DOM element

</v-click>

<br>

## Q7: 一個 component 有哪些可能會被觸發 re-render 的情形?

<br>

<v-click>

> #### 有兩種可能的情形：
> - #### component 本的有定義 state，且該 state 的 `setState` 方法被呼叫
> - #### component 的父代或祖父代 component 發生 re-render 

</v-click>

---
class: flex justify-center items-center

---

# 第二章回顧

---

# 畫面管理機制

2-6 單向資料流與一律重繪渲染策略


<div class="grid-container">
  <img
    src="/one-way-dataflow.svg"
    alt=""
  />
  <span>圖 2-6-1</span>
</div>

<br>

### 單向資料流
- 可維護性↑、可讀性↑、資料出錯風險↓、效能優化↑

<br>

### 一律重繪策略
- 資料更新後，一律清空畫面再重繪畫面
- 缺點：大量不必要的 DOM 操作導致效能問題

<v-click>

<div class="text-center">

## virtual DOM

</div>

</v-click>

<style>
.grid-container {
  display: grid;
  justify-items: center;
  grid-template-rows: auto auto;
}
</style>

<!-- 
- 在 2-6 介紹到，在眾多現代端框架或解決方案中，「單向資料流」已經成為主流，因為...
- 為了做到單向資料流，React 選擇使用「一律重繪」策略
- 但，全部都重繪實際 DOM 很浪費效能，所以改成重繪虛擬的 DOM -->

---

# virtual DOM

2-1 DOM 與 Virtual DOM
<br>
2-2 建構畫面的最小單位：React element
<br>
2-3 Render React element

<v-switch>
  <template #1>
    <div class="flex justify-center">
      <img
        src="/vDOM.svg"
        alt=""
      />
    </div>
  </template>
  <template #2>
    <div class="flex justify-center">
      <img
        src="/vDOM_2.svg"
        alt=""
      />
    </div>
  </template>
</v-switch>

<!-- 
- 因此，在 2-1 介紹了什麼是 DOM? 什麼是 virtual DOM?
- [click]在 React 中，React Element 是基於 virtual DOM 概念所實現的虛擬畫面結構元素，同時也是 React 畫面結構中的最小單位
- 而 React Element 是透過 createElement() 這個 function 產生出來的
- 最後這些 React Element 會再透過 react-dom 進行轉換與繪製，變成實際的 DOM -->

---

# JSX

2-4 JSX 根本不是在 Javacript 寫 HTML
<br>
2-5 JSX 語法規則脈絡與畫面渲染實用技巧

<div class="grid-container">
  <img
    class="w-200"
    src="/jsx.svg"
    alt=""
  />
  <span>圖 2-4-5</span>
</div>

<style>
.grid-container {
  display: grid;
  justify-items: center;
  grid-template-rows: auto auto;
}
</style>

<!-- 
- 但 createElement 其實使用上不太直觀，所以就有了 JSX 語法糖
- JSX 語法長得很像 HTML，讓開發者可以更方便、簡潔、易讀
- 程式碼中的 JSX 語法必須經過外部工具轉譯成 React.createElement，才能正常地被瀏覽器執行 -->

---

# Component

2-7 畫面組裝的藍圖：component 初探
<br>
2-8 React 畫面更新的發動機：state 初探
<br>
2-9 React 畫面更新的流程機制：reconciliation

<img
  src="/process_all.svg"
  alt=""
/>

<!-- 
- 根據需求，將畫面拆成多個 component
- component 是藍圖，用來產生 React element，也可以透過 props 來微調產生的 React element
- 而 component 的資料狀態，則是用 state 來實現
- 在第三章會再更仔細地介紹 state
- 第四章會介紹 Component 的生命週期與資料流
- 第五章則會介紹 useState 以外的其他 hook -->

---
class: flex justify-center items-center

---

# Thank you