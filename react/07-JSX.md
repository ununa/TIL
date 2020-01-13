# JSX와의 재회
- 브라우저는 JSX와 관련해 아무것도 모른다.
- JSX를 브라우저가 이해할 수 있는 언어로 변환해주는 바벨과 같은 툴이 필요하다. (트랜스파일 과정)
#### 이전 Card 관련 Component
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
        /* JSX 코드
        return(
            <div style={cardStyle}>
                <Square color={this.props.color} />
                <Label color={this.props.color} />
            </div>
        );
        */
        
        // 순수 자바스크립트 코드
        return React.createElement(
            'div',
            {style: cardStyle},
            React.createElement(Square, {color: this.props.color}),
            React.createElement(Label, {color: this.props.color})
        );
    }
}
```

## 기억해야 할 JSX의 특징
### 01. 표현식 평가
- JSX는 자바스크립트처럼 취급되며, 정적 콘텐츠만을 다루게 제한돼 있지 않다.
- 리턴되는 값을 동적으로 생성되게 할 수 있다.
- 해아 할 일은 표현식을 중괄호로 감싸는 것이 전부
``` js
class Stuff extends React.Component {
    render(){
        return(
            <h1>Boring {Math.random() * 100} content!</h1>
        )
    }
}
```

### 02. 복수의 엘리먼트 리턴
#### 방법1. 배열같은 식의 문법 사용
단일한 부모 엘리먼트 없이 P태그 세 개를 리턴
- key 속성과 고유의 값을 지정하면 리액트가 어떤 엘리먼트를 다뤄야 하는지, 그리고 변경이 발생했는지 더 잘 이해할 수 있다.
- key속성을 사용하지 않은 상태에서 개발자 도구 콘솔에 ```Warning: Each child in an array or iterator should have a uniqure "key" prop.``` 메세지가 뜬다면 사용하는게 낫다.
``` js
class Stuff extends React.Component {
    render(){
        return(
            [
                <p key="1">I am</p>,
                <p key="2">returning a list</p>,
                <p key="3">of things!</p>
            ]
        );
    }
}
```

#### 방법2. 프래그먼트(Fragments)
리액트 v16.2.0부터 추가됨
1. ```React.Fragment``` 컴포넌트는 실제로 DOM 엘리먼트로 생성 되지 않는다. 단지 HTML로 트랜스파일될 때 존재하지 않는 것으로 취급하라고 JSX에게 알려줄 뿐이다.
2. 아이템들이 배열에 담겨 리턴되는 것이 아니므로 쉼표나 다른 구분자가 필요 없다.
3. key 속성과 고유값을 지정할 필요가 없다. 그와 관련된 모든 사항은 물밑에서 알아서 관리된다. 
``` js
class Stuff extends React.Component {
    render(){
        return(
            <React.Fragment>
                <p>I am</p>
                <p>returning a list</p>
                <p>of things!</p>
            </React.Fragment>
        );
    }
}
```
#### React.Fragment 축약 구문
> 하지만 많은 도구에서 아직 지원하지 않기 때문에 React.Fragment를 넣어주자.
``` js
class Stuff extends React.Component {
    render(){
        return(
            <>
                <p>I am</p>
                <p>returning a list</p>
                <p>of things!</p>
            </>
        );
    }
}
```

### 03. 인라인 CSS 사용 불가
- JSX에서의 style 속성은 HTML에서의 style 속성과 다르게 동작하기 때문에 스타일 정보를 담은 객체를 참조해야 한다.
- 카멜 표기법으로 된 모든 CSS 속성과 값을 포함하는 letterStyle 객체를 style 속성에 지정하고 있다.
``` js
class Letter extends React.Component {
    render(){
        var letterStyle = {
            padding: 10,
            margin: 10,
            backgroundColor: this.props.bgcolor,
            color: '#333',
            display: 'inline-block',
            fontFamily: 'monospace',
            fontSize: 32,
            textAlign: 'center'
        };

        return(
            <div style={letterStyle}>
                {this.props.children}
            </div>
        );
    }
}
```

### 04. 주석
#### 주석이 표현식으로 해석 될 수 있게 중괄호로 감싸기
``` js
ReactDOM.render(
    <div>
        <Card color="#FFA737" />
        {/* 자식으로서의 주석 */}
    </div>,
    document.querySelector('#container')
);
```
#### 주석을 태그 안에 넣을 경우
중괄호로 감쌀 필요 없이 한 라인이나 여러 라인의 주석을 지정
``` js
ReactDOM.render(
    <div>
        <Card color="#FFA737" // 라인 끝에 넣은 주석
            /* 이 주석은
               여러 라인에
               걸쳐 있다. */
         />
    </div>,
    document.querySelector('#container')
);
```

### 05. 대소문자 구별
- HTML 엘리먼트를 나타날 때에는 소문자
- 컴포넌트를 나타날 때에는 대문자
- 대소문자 구별을 정확히 하지 않으면 리액트는 콘텐츠를 렌더링하지 않는다.
``` js
ReactDOM.render(
    <div>
        <section>
            <p>Something goes here!</p>
            <MyCustomComponent />
        </section>
    </div>,
    document.querySelector('#container')
);
```

## 어디서든 가능한 JSX
- JSX 코드로 초기화 되는 swatchComponent 변수는 render 함수 안에서 swatchComponent 변수가 사용될 때 초기화된다.
- 추후 자바스크립트를 사용해 JSX를 생성하고 조작하는 방법을 배우게 되면 이런식의 코딩을 더 많이 하게 될 것이다.
``` js
var swatchComponent = <Swatch color="#2f004f"></Swatch>;

ReactDOM.render(
    <div>
        {swatchComponent}
    </div>,
    document.querySelector('#container')
);
```
