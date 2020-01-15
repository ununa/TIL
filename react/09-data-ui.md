# 데이터에서 UI로

``` js
class Circle extends React.Component {
    render(){
        var circleStyle = {
            width: 100,
            height:100,
            display: 'inline-block',
            padding: 10,
            margin: 20,
            borderRadius: '50%',
            backgroundColor: this.props.bgColor
        }
        return(
            <div style={circleStyle}></div>
        )
    }
}
ReactDOM.render(
    <div>
        <Circle bgColor="#F9C240" />
    </div>,
    document.querySelector('#container')
);
```

## 어디든 가능한 JSX -2탄
``` js
var theCircle = <Circle bgColor="#F9C240" />

ReactDOM.render(
    <div>
        {theCircle}
    </div>,
    document.querySelector('#container')
);
```
- ```theCircle``` 변수에는 Circle 컴포넌트를 인스턴스화하기 위한 JSX가 담긴다.
- 이 변수가 ```ReactDOM.render``` 함수 안에서 평가되면 그 결과로 화면에 원이 보이게 된다.

``` js
function showCircle(){
    var colors = ['#393e41','#e94f37','#1c89bf','#a1d363'];
    var ran = Math.floor(Math.random() * colors.length);

    return <Circle bgColor={colors[ran]} />;
}

ReactDOM.render(
    <div>
        {showCircle()}
    </div>,
    document.querySelector('#container')
);
```
- ```Circle``` 컴포넌트를 리턴하는 함수

## 배열 다루기
``` js
var colors = ['#393e41','#e94f37','#1c89bf','#a1d363','#85ffc7','#297373','#ff8552','#a40e4c'];

var renderData = [];

for (var i = 0; i < colors.length; i++) {
    var color = colors[i];
    renderData.push(<Circle key={i + color} bgColor={color} />);
}

ReactDOM.render(
    <div>
        {renderData}
    </div>,
    document.querySelector('#container')
);
```
