# 組件 & Props
組件(component)可以將 UI 切分成一些的獨立的、可複用的部件，這樣你就只需專注於構建每一個單獨的部件。

組件從概念上看就像是函數，它可以接收任意的輸入值（稱之為"props"），並返回一個需要在頁面上展示的 React 元素。

## 組件(component)
在 ReactJS 中有兩種元件寫法，如下：

#### 1. 函式元件寫法

在函式中定義一個接收的參數 props。

- Functional components
  - 又稱 presentational、dumb、stateless components

```js
// Person.js (函式元件寫法)
import React from 'react';

const person =(props)=>{
  return <p> I'm {props.name} and I'am {props.age} yesrs old.</p>
}

export default person;
```

### 2. 類別元件寫法

若要存取 props 必須在前面加上 `this`。
- class-based components
  - 又稱 containers、smart、stateful components

```js
// Person.js (類別元件寫法)
import React from 'react';

class person extends React.Component {
  render() {
    return (
      <p> I'm {this.props.name} and I'am {this.props.age} yesrs old.</p>
    );
  }
}

export default person;
```

## React Props
在一般的 HTML 我們可以傳遞屬性，而在 React 中使用 Props 是固定不變的(只讀性)，它可以自定義變數傳入元件中並渲染出來 `{this.props.參數名稱}`，你可以把它想成是函式中傳遞的參數值。

### 組件渲染
在前面，我們遇到的React元素都只是DOM標籤：

```html
<div />
```

然而，React元素也可以是用戶自定義的組件：

```html
<Person />
```

當React遇到的元素是用戶自定義的組件，它會將JSX屬性作為單個對像傳遞給該組件，這個對象稱之為 `props`，以下為一個簡單的自定義組建[範例](https://codepen.io/gaearon/pen/YGYmEG?editors=0010)。

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

在背後 React 做了下面這些事情：
1. 我們對`<Welcome name="Sara" />`元素調用了ReactDOM.render()方法。
2. React將`{name: 'Sara'}`作為props傳入並調用Welcome組件。
3. Welcome組件將`<h1>Hello, Sara</h1>`元素作為結果返回。
4. React DOM將DOM更新為`<h1>Hello, Sara</h1>`。

> Tip: 組件名稱必須以大寫字母開頭。 例如，`<div />`表示一個DOM標籤，但`<Welcome />`表示一個組件，並且在使用該組件時你必須定義或引入它。

### 組合組件
組件可以在它的輸出中引用其它組件，有點類似洋蔥把每個組件包覆起來形成一個大組件，例如，我們可以創建一個 App 組件，用來多次渲染 Welcome 組件，以下[範例](https://codepen.io/gaearon/pen/KgQKPr?editors=0010)：

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```