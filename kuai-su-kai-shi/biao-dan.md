## 受控組件
在 HTML 當中，像 `<input>`， `<textarea>` 和 `<select>` 這些表單元素會維持自身狀態，並根據用戶輸入進行更新。但在 React 中，可變狀態通常保存在組件的狀態屬性中，並且只能用 `setState()` 方法進行更新。

## input 標籤
例如，我們想要使提交表單時輸出的名字，我們可以寫成`受控組件`的形式，以下[範例](https://codepen.io/gaearon/pen/VmmPgp?editors=0010)：

```jsx
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

由於 value 屬性是在我們的表單元素上設置的，因此顯示的值將始終為 React 中 this.state.value 的值。因此每次按鍵都會觸發 handleChange 來更新當前 React 的狀態，所展示的值也隨隨著不同用戶的輸入而更新。

使用`受控組件`，每個狀態的改變都有一個與之相關的處理函數。這樣就可以直接修改或驗證用戶輸入。例如，我們如果想限制輸入全部是大寫字母，可以我們將handleChange寫為如下：

```jsx
handleChange(event) {
  this.setState({value: event.target.value.toUpperCase()});
}
```