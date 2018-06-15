# 狀態提升
狀態提升的意思就是將子元件中的狀態(state)傳遞給父元件中去使用(props)， 達成資料共享，以下製作一個滾水沸騰的偵測當水溫超過100即沸騰，這邊我們建立一個 BoilingVerdict 的元件能夠判斷水溫是否沸騰，裡面的變數就是經由 Calculator 元件所傳遞過來的。

```jsx
function BoilingVerdict(props) {
  if (props.celsius >= 100) {
    return <p>The water would boil.</p>;
  }
  return <p>The water would not boil.</p>;
}
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    return (
      <fieldset>
        <legend>Enter temperature in Celsius:</legend>
        <input
          value={temperature}
          onChange={this.handleChange} />

        <BoilingVerdict
          celsius={parseFloat(temperature)} />

      </fieldset>
    );
  }
}
```

![](/assets/img2-9-1.png)

[範例](https://codepen.io/valscion/pen/VpZJRZ?editors=0010)

## 實作
這邊要實作一個攝氏與華氏的溫度轉換器，輸入攝氏溫度自動顯示華氏的溫度，相對地能夠輸入華氏溫度並自動顯示攝氏的溫度。



