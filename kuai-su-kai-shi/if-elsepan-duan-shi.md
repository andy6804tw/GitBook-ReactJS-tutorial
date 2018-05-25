# if-else判斷式
在 JSX 中可以自由地加入判斷式 `render()內return外` 並用變數儲存 JSX 內容，若要在渲染出來則用大括號放入變數顯示內容。

## 在return中加入判斷式

```js
import React, { Component } from 'react';

export default class Main extends Component {
  state = {
    name: '王小明'
  }
  render() {

    return (
      <div style={{ textAlign: 'center' }}>
        <h2>Hello</h2>
        {

          this.state.name === '王小明' ? <h1>{this.state.name} 歡迎光臨</h1> : <h1>Hello, Stranger.</h1>
        }
      </div>
    );
  }
}

```

## 使用 JavaScript 方式

```js
import React, { Component } from 'react';


export default class Main extends Component {
  render() {
    const getGreeting = (user) => {
      if (user) {
        return (
          <div>{user}
            <h1>歡迎光臨</h1>
          </div>
        );
      }
      return <h1>Hello, Stranger.</h1>;
    };
    return (
      <div style={{ textAlign: 'center' }}>
        <h2>Hello</h2>
        {
          getGreeting('王小明')
        }
      </div>
    );
  }
}
```