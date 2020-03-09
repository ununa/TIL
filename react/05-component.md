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




## 2020-03-09 내용 추가
### 간단한 컴포넌트
React 컴포넌트는 ```render()``` 라는 메서드를 구현하는데, 이것은 데이터를 입력받아 화면에 표시 할 내용을 반환하는 역할을 한다. 컴포넌트로 전달된 데이터는 ```render()``` 안에서 ```this.props```를 통해 접근할 수 있다.

``` js
class HelloMessage extends React.Component {
    render() {
        return(
            <div>
                Hello {this.props.name}
            </div>
        )
    }
}

ReactDOM.render(
    <HelloMessage name="ununa" />,
    document.getElementById('hello-example')
);
```

### 상태를 가지는 컴포넌트
컴포넌트는 ```this.props```를 이용해 입력 데이터를 다루는 것 외에도 ```this.state```로 접근하여 내부적인 상태 데이터를 가질 수 있다. 컴포넌트의 상태 데이터가 바뀌면 ```render()```가 다시 호출되어 마크업이 갱신된다.

``` js
class Timer extends React.Component {
    constructor(props) {
        super(props);
        this.state = { seconds: 0 };
    }

    tick() {
        this.setState(state => ({
            seconds: state.seconds + 1
        }));
    }

    componentDidMount() {
        this.interval = setInterval(() => this.tick(), 1000);
    }
}

ReactDOM.render(
    <Timer />,
    document.getElementById('timer-example')
);
```

### 애플리케이션
```props```와 ```state```를 사용해서 간단한 Todo 애플리케이션을 만들 수 있다. ```state```를 사용해 입력자가 입력한 텍스트와 할 일 목록을 관리하는데, 이벤트 핸들러들이 인라인으로 각각 존재하는 것처럼 보이지만, 실제로는 이벤트 위임을 통해 하나로 구현된다.

``` js
class TodoApp extends React.Component{
    constructor(props) {
        super(props);
        this.state = { items: [], text: '' };
        this.handleChange = this.handleChange.bind(this);
        this.handleSubmit = this.handleSubmit.bind(this);
    }

    render() {
        return(
            <div>
                <h3>TODO</h3>
                <TodoList items={this.state.items} />
                <form onSubmit={this.handleSubmit}>
                    <label htmlFor="new-todo">
                        What needs to be done?
                    </label>
                    <input
                        id="new-todo"
                        onChange={this.handleChange}
                        value={this.state.text}
                    />
                    <button>
                        Add #{this.state.items.length + 1}
                    </button>
                </form>
            </div>
        );
    }

    handleChange(e) {
        this.setState({ text: e.target.value });
    }

    handleSubmit(e) {
        e.preventDefault();
        if (!this.state.text.length) {
            return;
        }
        const newItem = {
            text: this.state.text,
            id: Date.now()
        };
        this.setState(state => ({
            items: state.items.concat(newItem),
            text: ''

        }));
    }
}


class TodoList extends React.Component {
    render() {
        return (
            <ul>
                {this.props.items.map(item => (
                    <li key={item.id}>{item.text}</li>
                ))}
            </ul>
        );
    }
}

ReactDOM.render(
    <TodoApp />,
    document.getElementById('todos-example')
);
```


### 외부 플러그인을 사용하는 컴포넌트
React는 유연하며 다른 라이브러리나 프레임워크를 함께 활용할 수 있다. 마크다운 라이브러리인 ```remarkable```을 사용해 ```<textarea>```의 값을 실시간으로 변환해보자.

``` js
class MarkdownEditor extends React.Component {
    constuctor(props) {
        super(props);
        this.handleChange = this.handleChange.bind(this);
        this.state = { value: "Hello, **world**!" };
    }

    handleChange(e) {
        this.setState({ value: e.target.value });
    }

    getRawMarkup() {
        const md = new Remarkable();
        return { __html: md.render(this.state.value) };
    }

    render() {
        return(
            <div className="MarkdownEditor">
                <h3>Input</h3>
                <label htmlFor="markdown-content">
                    Enter some markdown
                </label>
                <textarea
                    id="markdown-content"    
                    onChange={this.handleChange}
                    defaultValue={this.state.value}
                />
                <h3>Output</h3>
                <div
                    className="content"
                    dangerouslySetInnerHTML={this.getRawMarkup()}
                >
                </div>
            </div>
        );
    }
}

ReactDOM.render(
    <MarkdownEditor />,
    document.getElementById('markdown-example')
);
```


#### 예제: https://ko.reactjs.org/
