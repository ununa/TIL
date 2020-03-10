# DOM 엘리먼트 접근
리액트는 HTML 엘리먼트에 대한 DOM API에 접근할 수 있게 하는, ref라는 도구를 제공한다. 또한 페이지 안의 어떤 HTML 엘리먼트든 렌더링 할 수 있게 하는 포털이라는 기능도 제공.

## 컬러라이저 예제
> 목표: 폼이 제출되면 input 엘리먼트의 콘텐츠를 지우고 포커스를 갖게 하는 것.
``` html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Events</title>
<script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
<style>
#container {
    padding: 50px;
    background-color:#fff;
}

.colorSquare {
  width:242px;
  height:242px;
  margin-bottom:15px;
  box-shadow:0 0 25px 0 #333;
}

.colorArea input {
  padding:10px;
  border:2px solid #ccc;
  font-size:16px;
}

.colorArea button {
  padding:10px;
  margin:10px;
  border:2px solid #666;
  background-color:#666;
  font-size:16px;
  color:#fff;
}

.colorArea button:hover {
  border-color:#111;
  background-color:#111;
  cursor:pointer;
}

</style>
</head>
<body>

<div id="container"></div>

<script type="text/babel">
class Colorizer extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      color: '',
      bgColor: 'white'
    };

    this.colorValue = this.colorValue.bind(this);
    this.setNewColor = this.setNewColor.bind(this);
  }

  colorValue(e) {
    this.setState({
      color: e.target.value
    });
  }

  setNewColor(e) {
    this.setState({
      bgColor: this.state.color
    });

    e.preventDefault();
  }

  render(){
    var squareStyle = {
      backgroundColor: this.state.bgColor
    };

    return(
      <div className="colorArea">
        <div style={squareStyle} className="colorSquare"></div>
        <form onSubmit={this.setNewColor}>
          <input onChange={this.colorValue} placeholder="Enter a color value" ></input>
          <button type="submit">go</button>
        </form>
      </div>
    );
  }
}

ReactDOM.render(
  <div>
    <Colorizer />
  </div>,
  document.querySelector('#container')
);
</script>

</body>
</html>
```

## ref와의 첫 만남
- 이 render 메소드는 한 무더기의 JSX를 리턴하는데, 여기에는 컬러 값을 입력한 input 엘리먼트가 포함된다.
- 자바스크립트를 사용해 API를 호출 할 수 있게 input 엘리먼트의 DOM에 접근하는 작업을 해보자.
> ref(reference): HTML 엘리먼트와 JSX사이를 연결해준다.
``` js
render(){
    var squareStyle = {
      backgroundColor: this.state.bgColor
    };
    
    var self = this; // 추가됨

    return(
      <div className="colorArea">
        <div style={squareStyle} className="colorSquare"></div>
        <form onSubmit={this.setNewColor}>
          <input onChange={this.colorValue} 
                 ref={ // 콜백 함수(익명) 추가됨
                    function(el) {
                      self._input = el;
                    }
                 }
                 placeholder="Enter a color value"></input>
          <button type="submit">go</button>
        </form>
      </div>
    );
  }
```
- 보통은 현재 컴포넌트가 마운트되면 자동으로 호출될 자바스크립트 콜백 함수를 ```ref``` 속성 값으로 설정한다.
- ref 속성 값으로 단순히 DOM 엘리먼트의 참조를 저장하는 자바스크립트 함수를 지정한 것.
- 컴포넌트가 마운트되면 그 다음은 쉬운데, 컴포넌트 안의 어디서든 ```self._input```을 사용해 ```input``` 엘리먼트를 나타내는 HTML에 접근할 수 있다.
- 위 익명 함수는 컴포넌트가 마운트되면 호출되며, 최종 HTML DOM 엘리먼트에 대한 참조를 인자로 받는다.
- ```el```: 참조 인자. 어떤 이름이든 상관 없으면 ```_input```이라는 커스텀 속성에 DOM 엘리먼트의 값을 지정하는 일을 한다.
- 컴포넌트에 ```_input``` 속성을 만들기 위해 ```self``` 변수를 사용해 클로저(내부함수)를 만들었다.
- 여기서 ```this```는 콜백 함수가 아닌 컴포넌트를 참조한다.

``` js
  setNewColor(e) {
    this.setState({
      bgColor: this.state.color
    });
    
    this._input.focus(); // input 엘리먼트로 포커스가 가게 함.
    this._input.value = ""; // input 엘리먼트에 입력됐던 내용 삭제.

    e.preventDefault();
  }
```


## 포털 사용하기
- 포털이란? JSX를 페이지의 어느 곳으로든 DOM 엘리먼트로 렌더링시킬 수 있다.
- 사용방법은 ReactDOM.render 메소드와 매우 유사한데, 렌더링할 JSX를 지정하고, 렌더링해 보낼 대상 DOM 엘리먼트를 지정하면 된다.
``` html
<h1 id="colorHeading">Colorizer</h1>
```
``` css
#colorHeading {
    padding: 0;
    margin: 50px;
    margin-bottom: -20px;
    font-family: sans-serif;
}
```
``` js
// 추가
var heading = document.querySelector('#colorHeading');

class ColorLabel extends React.Component {
  render(){
    return ReactDOM.createPortal(
      ": " + this.props.color,
      heading
    )
  }
}

class Colorizer extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      color: '',
      bgColor: 'white'
    };

    this.colorValue = this.colorValue.bind(this);
    this.setNewColor = this.setNewColor.bind(this);
  }

  colorValue(e) {
    this.setState({
      color: e.target.value
    });
  }

  setNewColor(e) {
    this.setState({
      bgColor: this.state.color
    });

    e.preventDefault();
  }

  render(){
    var squareStyle = {
      backgroundColor: this.state.bgColor
    };

    return(
      <div className="colorArea">
        <div style={squareStyle} className="colorSquare"></div>
        <form onSubmit={this.setNewColor}>
          <input onChange={this.colorValue}
                 ref={
                   function(el) {
                     self._input = el;
                   }
                 }
                 placeholder="Enter a color value" ></input>
          <button type="submit">go</button>
        </form>
        <ColorLabel color={this.state.bgColor}/> // 추가
      </div>
    );
  }
}
```
- ColorLabel 이라는 컴포넌트를 인스턴스화했으며, state.bgColor 속성을 color 속성 값으로 설정했다.
- ReactDOM.createPortal()은 두 개의 인자를 받는다.
- 첫째는 출력될 내용의 JSX
- 둘째는 그 JSX 출력시킬 대상 DOM 엘리먼트 이다.
- ★ h1 엘리먼트가 container div를 출력하는 앱 범위 밖에 있다는 점.
- ★ 포털을 사용함으로써 부모와 자식으로 이뤄진 기존 계층 구조에 갇히지 않고 페이지의 어느 엘리먼트든 직접 접근이 가능하다.






