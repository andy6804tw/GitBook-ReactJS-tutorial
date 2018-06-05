# if-else判斷式
在 JSX 中可以自由地加入判斷式 `render()內return外` 並用變數儲存 JSX 內容，若要在渲染出來則用大括號放入變數顯示內容。

## 元素變量
```jsx
class Main extends React.Component {
  state = {
    name: '王小明'
  }
  render() {
    let greet = null;
    if (this.state.name === '王小明') {
      greet = <h1>{this.state.name} 歡迎光臨</h1>;
    } else {
      greet = <h1>Hello, Stranger.</h1>;
    }
    return (
      <div style={{ textAlign: 'center' }}>
        <h2>Hello</h2>
        {greet}
      </div>
    );
  }
}

ReactDOM.render(
  <Main />,
  document.getElementById('root')
);
```

![](/assets/img2-2-1.png)



## 問號運算符
在 return 中加入判斷式

```jsx
class Main extends React.Component {
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

ReactDOM.render(
  <Main />,
  document.getElementById('root')
);
```

![](/assets/img2-2-1.png)

## 運算符&&

```jsx
class Main extends React.Component {
  state = {
    name: '王小明'
  }
  render() {

    return (
      <div style={{ textAlign: 'center' }}>
        <h2>Hello</h2>
        {
          this.state.name === '王小明' && <h1>{this.state.name} 歡迎光臨</h1>
        }
      </div>
    );
  }
}
ReactDOM.render(
  <Main />,
  document.getElementById('root')
);
```

![](/assets/img2-2-1.png)

## 使用 Function 方式

```jsx
class Main extends React.Component {  `render() {
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
ReactDOM.render(
  <Main />,
  document.getElementById('root')
);

```

![](/assets/img2-2-2.png)
