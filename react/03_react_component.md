## 함수에 대한 짧은 복습
함수는 코드를 더 명확하고 재사용 가능하게 만든다. 개념적으로 함수는 리액트 컴포넌트와 많은 부분을 표면적으로 공유한다.

#### 계산하는 함수
``` js
function getDistance(speed, time) {
  var result = speed * time;
  alert(result);
}

getDistance(10, 5);
getDistance(85, 1.5);
getDistance(12, 9);
getDistance(42, 21);
```

#### 함수 안에서 다른 함수를 호출하기
어떤 함수에서 다른 함수의 호출이 가능하다는 점은 함수가 해야 할 일을 명확히 분리할 수 있게 한다. 
``` js
function formatDistance(distance) {
  return distance + 'km';
}

function getDistance(speed, time) {
  var result = speed * time;
  alert(formatDistance(result));
}
```

## 리액트 컴포넌트와의 첫 만남
리액트 컴포넌트는 JSX를 통해 HTML 엘리먼트를 출력할 수 있는 재사용 가능한 자바스크립트 덩어리. 
#### 기본 코드
``` html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>React Sample</title>
<script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
</head>
<body>

<div id="container"></div>

<script type="text/babel">
ReactDOM.render(
    <div>
        <p>Hello, world!</p>
    </div>,
    document.querySelector('#container')
);
</script>

</body>
</html>
```
### Hello, World! 컴포넌트 만들기
- 컴포넌트가 제대로 작동되려면 필수 속성인 ```render```를 사용한다.
- ```ReactDOM.render```의 경우와 마찬가지로 컴포넌트 안의 ```render``` 역시 JSX를 처리한다.
``` js
class HelloWorld extends React.Component {
    render(){
        return <p>Hello, world!</p>
    }
}
```

#### ReactDOM.render에서 호출하기
- ```<HelloWorld/>```는 완벽히 통제 가능한 기능의 새로운 HTML 태그라고 생각하자.
- ```<HelloWorld/>```를 ```<div>```로 감쌀수 있으며, 여러 번 호출 가능하다.
``` js
ReactDOM.render(
  <div>
    <HelloWorld/>
    <HelloWorld/>
  </div>,
  document.querySelector('#container')
)
```
### 속성지정
- 컴포넌트에서도 함수와 마찬가지로 인자를 전달해 그에 맞게 동작하게끔 할 수 있다. 
- 함수에서의 ```인자```는 컴포넌트에선 ```속성(property)``` 라고 부른다.
- 원하는 만큼 속성을 추가 할 수 있음
#### 첫 번째 작업: 컴포넌트 정의변경
- 컴포넌트 속성 이름: ```greetTarget```
- 모든 컴포넌트가 접근할 수 있는 ```props```라는 속성을 통해 호출하게 변경.
- JSX에서는 표현식(expression)으로 처리되게 하려면 반드시 중괄호```{}```로 감싸야 한다.  그렇지 않으면 this.props.greetTarget이라는 텍스트가 그대로 출력되기 때문이다.
```js
class HelloWorld extends React.Component {
    render(){
        return <p>Hello, {this.props.greetTarget}!</p>
    }
}
```
#### 두 번째 작업: 컴포넌트 호출 수정
- 호출시속성 값을전달하게하는일.
- 컴포넌트 속성의 이름과 동일한 이름의 엘리먼트 속성을 추가함으로써 가능하다.
```js
ReactDOM.render(
    <div>
        <HelloWorld greetTarget="ununa"/>
        <HelloWorld greetTarget="dodoh"/>
    </div>,
    document.querySelector('#container')
);
```

### 자식 다루기
- JSX 컴포넌트는 보통의 HTML 엘리먼트와 매우 유사하다.
#### 예제 1.
``` js
<CleverComponent foo="bar">
  <p>...</p>
</CleverComponent>
```
#### 예제 2.
- 버튼안에 자식을 감싸고 있는 ```Buttonify```컴포넌트
``` js
class Buttonify extends React.Component {
  render(){
    return(
      <div>
        <button type="{this.props.behavior}">{this.props.children}</button>
      </div>
    );
  }
}

ReactDOM.render(
  <div>
    <Buttonify behavior="submit">SEND DATA</Buttonify>
  </div>,
  document.querySelector('#container')
)
```



