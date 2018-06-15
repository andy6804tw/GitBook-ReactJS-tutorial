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

**小幫手**
由於我們要實作的功能是輸入第一個input自動的第二個input換上並補上結果如下圖，所以我們實作方式就是建立一個 `<TemperatureInput>` 元件提供使用者輸入框，內部的 value 是經由 props 傳遞，最外層用一個 `<Calculator>` 元件包起來。

* React在DOM原生組件`<input>`上調用指定的`onChange`函數。在本例中，指的是`TemperatureInput`組件上的`handleChange`函數。
* `TemperatureInput`組件的`handleChange`函數會在值發生變化時調用`this.props.onTemperatureChange()`函數。這些props屬性，像`onTemperatureChange`都是由父組件`Calculator`提供的。
* 當最開始渲染時，`Calculator`組件把內部的`handleCelsiusChange`方法指定給攝氏輸入組件`TemperatureInput`的`onTemperatureChange`方法，並且把`handleFahrenheitChange`方法指定給華氏輸入組件`TemperatureInput`的`onTemperatureChange` 。兩個`Calculator`內部的方法都會在相應輸入框被編輯時被調用。
* 在這些方法內部，`Calculator`組件會讓React使用編輯輸入的新值和當前輸入框的溫標來調用`this.setState()`方法來重渲染自身。 * React會調用`Calculator`組件的`render`方法來識別UI界面的樣子。基於當前溫度和溫標，兩個輸入框的值會被重新計算。溫度轉換就是在這裡被執行的。
* 接著React會使用`Calculator`指定的新props來分別調用`TemperatureInput`組件，React也會識別出子組件的UI界面。
* React DOM 會更新DOM來匹配對應的值。我們編輯的輸入框獲取新值，而另一個輸入框則更新經過轉換的溫度值。

![Demo](https://doc.react-china.org/react-devtools-state-ef94afc3447d75cdc245c77efb0d63be.gif)

[範例](https://github.com/ReactXLab/temperature-calculate)

