# 事件處理

- React事件綁定屬性的命名採用駝峰式寫法，而不是小寫。
    - 例：callFunction()
- 如果採用 JSX 的語法你需要傳入一個函數作為事件處理函數，而不是一個字符串(DOM元素的寫法)

**傳統事件處理**
```html
<button onclick="activateLasers()">
  Activate Lasers
</button>
```

**React事件處理**
```html
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

在React中另一個不同是你不能使用返回false的方式阻止默認行為。你必須明確的使用preventDefault。例如，傳統的HTML中阻止鏈接默認打開一個新頁面，你可以這樣寫：

```html
<a href="#" onclick="console.log('The link was clicked.'); return false">
  Click me
</a>
```

在React，應該這樣來寫：

```jsx
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```

## 製作一個開關按鈕事件
當你使用ES6 class語法來定義一個組件的時候，事件處理器會成為類的一個方法。例如，下面的Toggle組件渲染一個讓用戶切換開關狀態的按鈕：

```jsx
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```

[範例](https://codepen.io/gaearon/pen/xEmzGg?editors=0011)

## 兩種事件處理方法
1.使用箭頭函數

```jsx
<button onClick={(e) => this.handleClick(e)}>Click me</button>
```

2.綁定 this

```jsx
<button onClick={this.handleClick.bind(this)}>Click me</button>
```

## 事件傳遞參數

1.使用箭頭函數

```jsx
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
```

2.綁定 this

```jsx
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

上面兩個例子中，參數e作為React事件對象將會被作為第二個參數進行傳遞。通過箭頭函數的方式，事件對象必須顯式的進行傳遞，但是通過bind的方式，事件對像以及更多的參數將會被隱式的進行傳遞。

值得注意的是，通過bind方式向監聽函數傳參，在類組件中定義的監聽函數，事件對象e要排在所傳遞參數的後面，例如:


```jsx
class Popper extends React.Component{
    constructor(){
        super();
        this.state = {name:'Hello world!'};
    }
    
    preventPop(name, e){    //事件對象e要放在最後
        e.preventDefault();
        alert(name);
    }
    
    render(){
        return (
            <div>
                <p>hello</p>
                {/* Pass params via bind() method. */}
                <a href="https://reactjs.org" onClick={this.preventPop.bind(this,this.state.name)}>Click</a>
            </div>
        );
    }
}
```