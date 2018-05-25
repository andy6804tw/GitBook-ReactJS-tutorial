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