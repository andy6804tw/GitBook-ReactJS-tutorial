# 組合vs繼承
React具有強大的組合模型，官方建議我們使用組合而不是繼承來復用組件之間的代碼。

## 包含關係
一些組件不能提前知道它們的子組件是什麼，或是想客製化裡面的內容，這時就可以在元件內使用 children 屬性將子元素直接傳遞到輸出，以下[範例](http://codepen.io/gaearon/pen/ozqNOV?editors=0010)。

```jsx
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}

function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}
```

![](/assets/img2-10-1.png)


再來這個情況可能不常見，但有時你可能需要在元件中有多個入口，這種情況下你可以使用自己約定的 props 而不是 children，以下[範例](https://codepen.io/gaearon/pen/gwZOJp?editors=0010)：

```jsx
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={
        <Contacts />
      }
      right={
        <Chat />
      } />
  );
}
```

![](/assets/img2-10-2.png)

`<Contacts />` 和 `<Chat />` 這樣的 React 元素都是物件，所以你可以像任何其他元素一樣傳遞它們。

## 特殊實例
有時我們認為組件是其他組件的特殊實例(special cases)。例如，會我們說 WelcomeDialog 的英文 Dialog 的特殊實例。

在React中，這也是通過組合來實現的，通過配置屬性用較特殊的組件來渲染較通用的組件。

```jsx
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}

function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
    </FancyBorder>
  );
}

function WelcomeDialog() {
  return (
    <Dialog
      title="Welcome"
      message="Thank you for visiting our spacecraft!" />

  );
}
```

![](/assets/img2-10-3.png)

[範例](http://codepen.io/gaearon/pen/kkEaOZ?editors=0010)