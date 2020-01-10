# 리액트 스타일링
리액트의 핵심 아이디어 중 하나는 앱의 비주얼 부품은 독립적이며, 재사용 가능해야하기때문에 CSS도 독립적인 것이 좋다.

## 알파벳 모음 보여주기
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
class Letter extends React.Component {
    render(){
        return (
            <div>
                {this.props.children}
            </div>
        )
    }
}

ReactDOM.render(
    <div>
        <Letter>A</Letter>
        <Letter>E</Letter>
        <Letter>I</Letter>
        <Letter>O</Letter>
        <Letter>U</Letter>
    </div>,
    document.querySelector('#container')
);
</script>

</body>
</html>
```

## 리액트 방식의 스타일링
리액트는 인라인 방식의 스타일링을 선호함. 이렇게 하는 것이 비주얼 컴포넌트의 재사용성을 더욱 높이는 일이다. 
### 스타일 객체 만들기
1. 한 단어로 된 CSS속성```(padding,margin,color 등)```은 그대로 사용한다.
2. 대시(-)로 연결된 여러 단어로 이뤄진 css 속성```(background-color, font-family, border-radius 등)```카멜 표기법(camel case)을 사용한다.
``` js
class Letter extends React.Component {
    render(){
        var letterStyle = {
            padding: 10,
            margin: 10,
            display: 'inline-block',
            backgroundColor: this.props.bgcolor, // 아래 배경색 커스터마이징과 연동
            textAlign: 'center',
            fontSize: 32,
            fontFamily: 'monospace',
            color: '#333'
        };
        return (
            <div style={letterStyle}> // 중괄호 안에 넣어 스타일 객체 지정.
                {this.props.children}
            </div>
        )
    }
}
```

### 배경색 커스터마이징
1. ```bgcolor``` 속성이 없으면 ```backgroundColor```값만 빠진 채 랜더링 된다.

``` js
ReactDOM.render(
    <div>
        <Letter>A</Letter>
        <Letter bgcolor="#ff605f">E</Letter>
        <Letter bgcolor="#ffd52e">I</Letter>
        <Letter bgcolor="#49dd8e">O</Letter>
        <Letter bgcolor="#ae99ff">U</Letter>
    </div>,
    document.querySelector('#container')
);
```








