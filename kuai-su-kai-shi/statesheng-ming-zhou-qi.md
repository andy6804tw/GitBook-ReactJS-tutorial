# State & 生命週期
React 中有兩個東西會控制到元件分別是 props 和 state， props 是由父元件傳入，在 component 中，它是不會被改變的，而要改變的資料會放在我們今天要介紹的 state。

## React state
state 比較像是 component 內部的變數，是一個 JavaScript 物件保留字，雖然 props 允許您將數據傳遞到 component（並因此觸發UI更新），但狀態用於更改 component，以及從內部狀態。更改狀態也會觸發 UI 更新。