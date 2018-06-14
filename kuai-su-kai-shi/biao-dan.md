## 受控組件
在 HTML 當中，像 `<input>`， `<textarea>` 和 `<select>` 這些表單元素會維持自身狀態，並根據用戶輸入進行更新。但在 React 中，可變狀態通常保存在組件的狀態屬性中，並且只能用 `setState()` 方法進行更新。

## input標籤
在HTML當中，`<input>` 標籤通常是表單供使用者輸入相關資訊，例如姓名、電話、住址、帳密......等有許多種 type 形式。

```html
<form>
  <label>
    Name:
    <input type="text" name="name" />
  </label>
  <input type="submit" value="Submit" />
</form>
```

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

## textarea標籤
在HTML當中，`<textarea>` 元素通過子節點來定義它的文本內容

```html
<textarea>
  Hello there, this is some text in a text area
</textarea>
```

在 React 中 `<textarea> ` 以 `value` 屬性值來存放文字內容，使用方式跟 `<input>` 極為相似。

```jsx
class EssayForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 'Please write an essay about your favorite DOM element.'
    };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('An essay was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <textarea value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

## select 標籤
在HTML當中，`<select>` 會創建一個下拉列表，以下示範原生 HTML 下拉列表。

```html
<select>
  <option value="grapefruit">Grapefruit</option>
  <option value="lime">Lime</option>
  <option selected value="coconut">Coconut</option>
  <option value="mango">Mango</option>
</select>
```

在 React 中 `<select>` 的 `value` 值代表預設被選取的內容 `onChange` 會持續監聽被選擇的內容即時做 state 更新，以下[範例](https://codepen.io/gaearon/pen/JbbEzX?editors=0010)：。

```jsx
class FlavorForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: 'coconut'};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('Your favorite flavor is: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Pick your favorite La Croix flavor:
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="grapefruit">Grapefruit</option>
            <option value="lime">Lime</option>
            <option value="coconut">Coconut</option>
            <option value="mango">Mango</option>
          </select>
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

> 小結 `<input type="text">`、`<textarea>`、`<select>` 使用方法都都十分類似，都他們通過傳入一個 value 屬性來實現對組件的控制。

## 多個input標籤
當有處理多個受控的 input 元素時，可以你給通過每個元素添加一個 name 屬性，讓來處理函數根據event.target.name 的值來選擇做什麼並更新其狀態(state)，以下[範例](https://codepen.io/gaearon/pen/wgedvV?editors=0011)：

```jsx
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}
```

注意我們如何使用ES6的當中計算屬性名語法來更新與給定輸入側名稱相對應的狀態鍵：

```jsx
this.setState({
  [name]: value
});
```