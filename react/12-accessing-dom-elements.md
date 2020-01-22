# DOM 엘리먼트 접근
리액트는 HTML 엘리먼트에 대한 DOM API에 접근할 수 있게 하는, ref라는 도구를 제공한다. 또한 페이지 안의 어떤 HTML 엘리먼트든 렌더링 할 수 있게 하는 포털이라는 기능도 제공.

## 컬러라이저 예제
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
ref(reference): HTML 엘리먼트와 JSX사이를 연결해준다.

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
                 ref={ // 추가됨
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








