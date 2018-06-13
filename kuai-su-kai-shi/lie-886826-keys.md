# 列表 & Keys

## 渲染多個元件素(Map)
一個陣列或物件中有多筆資料我們可以藉由 ES6 的 map 來走訪所有元素，以下[範例](https://codepen.io/gaearon/pen/GjPyQr?editors=0011)。

```jsx
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((numbers) =>
  <li>{numbers}</li>
);

ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);
```

![](/assets/img2-7-1.png)

## 列表元件
通常我們會取得多筆陣列資料，我們會以 prop 傳遞給元件，藉由元件內部 map 來做元素渲染，以下[範例](https://codepen.io/gaearon/pen/jrXYRR?editors=0011)。

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

當你創建一個元素時，必須包括一個特殊的key屬性，所以在每個 `<li>` 標籤中要註明每個 `key`，下一節會更詳細說明。

## Keys
Keys可以在DOM中的某些元素被增加或刪除的時候幫助React識別哪些元素發生了變化。因此你應當給數組中的每一個元素賦予一個確定的標識。

```jsx
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

一個元素的key最好是這個元素在列表中擁有的一個獨一無二的字符串。通常，我們使用來自數據的id作為元素的key:

```jsx
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```

當元素沒有確定的id時，你可以使用他的序列號索引 index 作為 key

```jsx
const todoItems = todos.map((todo, index) =>
  // Only do this if items have no stable IDs
  <li key={index}>
    {todo.text}
  </li>
);
```

>如果列表可以重新排序，我們不建議使用索引來進行排序，因為這會導致渲染變得很慢。

## 用keys提取元件
key的正確使用方式，以下[範例](https://codepen.io/rthor/pen/QKzJKG?editors=0010) :

```jsx
function ListItem(props) {
  // 正確！這裏不需要指定key:
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // 正確！key應該在元件的上下文中被指定
    <ListItem key={number.toString()}
              value={number} />

  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

>當你在map()方法的內部調用元件時，你最好隨時記得為每一個元素加上一個獨一無二的key。

## 在jsx中嵌入map()
在上面的範例中我們使用元素變量方式使用 map 渲染：

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />

  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

JSX 允許在大括號中嵌入任何表達式，所以我們可以在map()中這樣使用：

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />

      )}
    </ul>
  );
}
```

[範例](https://codepen.io/gaearon/pen/BLvYrB?editors=0010)