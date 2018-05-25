# 組件 & Props
組件(component)可以將UI切分成一些的獨立的、可複用的部件，這樣你就只需專注於構建每一個單獨的部件。

組件從概念上看就像是函數，它可以接收任意的輸入值（稱之為"props"），並返回一個需要在頁面上展示的 React 元素。

## 兩種元件寫法

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