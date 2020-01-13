# 복잡한 컴포넌트 제작
컴포넌트의 또 다른 주요한 강점은 바로 결합성(composability)이다. 즉, 여러 컴포넌트를 조합해 더 복잡한 컴포넌트를 만들 수 있다는 의미.

## 비주얼 엘리먼트에서 컴포넌트로
컬러 팔레트 카드 만들기. 만들기 위해선 두 단계가 필요하다.
1. 주요 비주얼 요소의 식별
2. 컴포넌트로 만들 대상의 식별

#### 주요 비주얼 요소 식별
- 우리가 다룰 모든 비주얼 요소를 식별하는 일이다. 
- 상세 구현 내용은 무시하고, 비주얼 요소를 나눌 때는 HTML과 CSS 조합을 기준으로 하지 말아야 한다.


#### 컴포넌트 식별
- 식별한 비주얼 요소 중에 어떤 것을 컴포넌트로 만들지 따져봐야 한다. 
- 컴포넌트로 만들 비주얼 요소를 선별하는 기법은 바로 하나의 컴포넌트는 하나의 역할만 해야한다.

## 컴포넌트 작성
``` html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>React Sample</title>
<script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
<style>
#container {
    padding: 50px;
    background-color:#fff;
}
</style>
</head>
<body>

<div id="container"></div>

<script type="text/babel">

ReactDOM.render(
    <div>
        
    </div>,
    document.querySelector('#container')
);
</script>

</body>
</html>
```

## 계획대로 3개의 컴포넌트 정의하기
### 각각 Card, Label, Square로 하기
``` js
class Square extends React.Component {
    render(){
        return(
            <br/>
        );
    }
}
class Label extends React.Component {
    render(){
        return(
            <br/>
        );
    }
}
class Card extends React.Component {
    render(){
        return(
            <br/>
        );
    }
}
```

### 카드 컴포넌트
``` js
class Card extends React.Component {
    render(){
        var cardStyle = {
            height: 200,
            width: 150,
            padding: 0,
            backgroundColor: '#fff',
            boxShadow: '0px 0px 5px #666'
        }
        return(
            <div style={cardStyle}>

            </div>
        );
    }
}
ReactDOM.render(
    <div>
        <Card />
    </div>,
    document.querySelector('#container')
);
```

### Square 컴포넌트
``` js
class Square extends React.Component {
    render(){
        var squareStyle = {
            height: 150,
            backgroundColor: '#ff6663'
        }
        return(
            <div style={squareStyle}>

            </div>
        );
    }
}
class Card extends React.Component {
    render(){
        var cardStyle = {
            height: 200,
            width: 150,
            padding: 0,
            backgroundColor: '#fff',
            boxShadow: '0px 0px 5px #666'
        }
        return(
            <div style={cardStyle}>
                <Square /> // 추가됨
            </div>
        );
    }
}
```


### Label 컴포넌트
``` js
class Label extends React.Component {
    render(){
        var labelStyle = {
            fontFamily: 'sans-serif',
            fontWeight: 'bold',
            padding: 13,
            margin: 0
        }
        return(
            <p style={labelStyle}>#FF6663</p>
        );
    }
}
class Card extends React.Component {
    render(){
        var cardStyle = {
            height: 200,
            width: 150,
            padding: 0,
            backgroundColor: '#fff',
            boxShadow: '0px 0px 5px #666'
        }
        return(
            <div style={cardStyle}>
                <Square />
                <Label /> // 추가됨
            </div>
        );
    }
}
```

## 속성전달
1. 하드코딩 된 컬러값을 ```this.props.color```를 이용해서 접근해보자.
2. 부모 컴포넌트에 속성을 지정하고 모든 자손이 자동으로 그 속성을 얻을 수 있게 하는 적절한 방법은 존재 하지 않는다.
3. 자식 컴포넌트에 속성 값을 전달하는 올바른 방법이란, 부모 컴포넌트 각각이 속성 값을 일일이 전달해주는 걸 말한다.
``` js
class Square extends React.Component {
    render(){
        var squareStyle = {
            height: 150,
            backgroundColor: this.props.color //-> this.props.color 추가
        }
        return(
            <div style={squareStyle}>

            </div>
        );
    }
}
class Label extends React.Component {
    render(){
        var labelStyle = {
            fontFamily: 'sans-serif',
            fontWeight: 'bold',
            padding: 13,
            margin: 0
        }
        return(
            <p style={labelStyle}>{this.props.color}</p> //-> this.props.color 추가
        );
    }
}
class Card extends React.Component {
    render(){
        var cardStyle = {
            height: 200,
            width: 150,
            padding: 0,
            backgroundColor: '#fff',
            boxShadow: '0px 0px 5px #666'
        }
        return(
            <div style={cardStyle}>
                <Square color={this.props.color} /> //-> this.props.color 추가
                <Label color={this.props.color} /> //-> this.props.color 추가
            </div>
        );
    }
}
ReactDOM.render(
    <div>
        <Card color="#FFA737" /> //-> color값 바뀜
    </div>,
    document.querySelector('#container')
);
```
이와 같은 방식으로 변경하면 Card 컴포넌트를 호출할 때 원하는 컬러 헥스 값을 지정 할 수 있다.

## 컴포넌트 결합성의 비밀
- 일반화 시키면, 작은 HTML덩어리를 리턴하는 게 컴포넌트가 하는 일의 전부이다.
- 각 컴포넌트의 ```render``` 함수는 또 다른 컴포넌트의 ```render``` 함수에게 리턴한다.
- 모든 HTML 덩어리들은 최종적으로 DOM에 밀어 넣어 거대한 덩어리가 될 때까지 쌓이는데 이게 컴포넌트의 재사용성과 결합성이 가능하게 된 이유이다.
