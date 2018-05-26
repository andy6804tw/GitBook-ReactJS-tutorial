# State & 生命週期
React 中有兩個東西會控制到元件分別是 props 和 state， props 是由父元件傳入，在 component 中，它是不會被改變的，而要改變的資料會放在我們今天要介紹的 state。

## React state
state 比較像是 component 內部的變數，是一個 JavaScript 物件保留字，雖然 props 允許您將數據傳遞到 component（並因此觸發UI更新），但 state 用於更改 component，以及從內部狀態。更改狀態也會觸發 UI 更新。

## 範例
目前為止我們學會如何透過簡單 DOM 元素渲染一個時鐘

```jsx
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

### 自定義組件並加入 props
首先我們來複習前面幾章所教的，我們改寫上面寫法使用 Functional components，並將時間封裝成一個 Clock 元件，並將時間以 props 方式傳入。

```jsx
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}
function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

各位可以發現我們是使用 props 方式將時間不斷更新傳入

```jsx
<Clock date={new Date()} />
```

是否可以直接向下面這樣寫呢？答案是可以使用 `state` 來解決！

```jsx
<Clock />
```


### 使用 status 改寫
`status` 與 `props` 十分相似，但是 status 是私有的，完全受控於當前組件，然而要使用 status 必須要使用 class-based components 寫法。

```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

[範例](https://codepen.io/gaearon/pen/KgQpJd?editors=0010)執行後你會發先時間不會動！沒錯目前只完成利用 status 取得目前時間，接下來我們要使用 React 的生命週期來每秒更新 status。

![](/assets/img2-5-1.png)


### 將生命週期方法添加到 Class 中


```jsx
// 掛載
componentDidMount() {

  }
// 卸載
componentWillUnmount() {

  }
```

最終結果，[範例](http://codepen.io/gaearon/pen/amqdNA?editors=0010)：

```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

讓我們快速回顧一下發生了什麼以及調用方法的順序：

1. 當<Clock />被傳遞給ReactDOM.render()時，React調用Clock組件的構造函數。由於Clock需要顯示當前時間，所以使用包含當前時間的對象來初始化this.state。我們稍後會更新此狀態。

2. React然後調用Clock組件的render()方法。這是React了解屏幕上應該顯示什麼內容，然後React更新DOM以匹配Clock的渲染輸出。

3. 當Clock的輸出插入到DOM中時，React調用componentDidMount()生命週期鉤子。在其中，Clock組件要求瀏覽器設置一個定時器，每秒鐘調用一次tick()。

4. 瀏覽器每秒鐘調用tick()方法。在其中，Clock組件通過使用包含當前時間的對象調用setState()來調度UI更新。通過調用setState()，React知道狀態已經改變，並再次調用render()方法來確定屏幕上應當顯示什麼。這一次，render()方法中的this.state.date將不同，所以渲染輸出將包含更新的時間，並相應地更新DOM。

5. 一旦Clock組件被從DOM中移除，React會調用componentWillUnmount()這個鉤子函數，定時器也就會被清除。


## state 的使用方法

### 建立 state 
1.使用建構子

```jsx
constructor(props) {
    super(props);
    this.data = 'Hello';
}
```

2.精簡方式
```jsx
state = {
    data: 'Hello'
}
```

### 更新 state

- 錯誤方式
```jsx
// Wrong
this.state.data = 'Hello World!';
```

- 正確方式
```jsx
// Correct
this.setState({data: 'Hello World!'});
```



### state 非同步更新
`this.props` 和 `this.state` 是異步更新的，不應該依靠它們的值來計算下一個狀態，而是像下面這樣。

```jsx
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));
```