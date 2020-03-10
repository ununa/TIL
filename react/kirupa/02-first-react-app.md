## 00. ReactDOM.render
```render``` 메소드는 두 개의 인자를 받는다.
1. 화면에 출력하고 싶은 HTML (즉, JSX)
2. 그 JSX를 렌더링해 보여줄 DOM 안의 위치
#### 방법1. 내부 입력
```js
ReactDOM.render(
    <h1>Hello, world</h1>,
    document.querySelector("#root")
);
```
#### 방법2. 외부에서 불러오기
```js
const element = <h1>Hello, world</h1>;
const _root = document.querySelector("#root");

ReactDOM.render(
    element,
    _root
);
```
