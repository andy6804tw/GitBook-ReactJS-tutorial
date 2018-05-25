# 元素渲染

首先我們在一個 HTML 頁面中添加一個 id="root" 的 `<div>`，在此div 中的所有內容都將由React DOM 來管理，所以我們將其稱之為“根” DOM 節點。

```html
<div id="root"></div>
```

要將React元素渲染到根DOM節點中，我們通過把它們都傳遞給ReactDOM.render()的方法來將其渲染到頁面上，以下為一個簡單[範例](https://codepen.io/gaearon/pen/rrpgNB?editors=1010)。

```js
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

![](/assets/img2-3-1.png)


## 更新元素渲染
這邊時做一個[小時鐘](https://codepen.io/gaearon/pen/gwoJZk?editors=0010)，透過 setInterval() 方法，每秒鐘調用一次 ReactDOM.render()。

```js
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

ReactJS 有很厲害的渲染機制，它只會更新必要的部分。

![](https://doc.react-china.org/granular-dom-updates-c158617ed7cc0eac8f58330e49e48224.gif)


