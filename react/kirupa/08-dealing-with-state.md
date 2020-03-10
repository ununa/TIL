# 상태 다루기
지금까지 만든 컴포넌트는 무상태(stateless) 컴포넌트였다. 즉, 한 번 설정되면 변하지 않는 속성처럼 사용되었으나, 많은 경우에는 그렇게 할 수 없을 것이다.  
컴포넌트에 변경되는 데이터를 저장해야 하는데, 그 데이터를 바로 상태(state)라고 한다.

## 상태 사용하기
- 모든 일이 벌어지는 장소는 ```LightningCounter``` 컴포넌트
- ```LightningCounterDisplay``` 컴포넌트를 DOM안의 ```container``` 엘리먼트에 밀어 넣고 있다.
- 최종 결과는 ```LightningCounterDisplay```와 ```LightningCounter``` 컴포넌트, 그리고 ```ReactDOM.render``` 메소드가 조합된 마크업이다.
``` js
class LightningCounter extends React.Component {
    render(){
        return(
            <h1>Hello!</h1>
        );
    }
}
class LightningCounterDisplay extends React.Component {
    render(){
        var commonStyle = {
            margin: 0,
            padding: 0
        };

        var divStyle = {
            width: 250,
            padding: 40,
            backgroundColor: '#020202',
            borderRadius: 10,
            textAlign: 'center',
            fontFamily: 'sans-serif',
            color: '#999'
        };

        var textStyle = {
            emphasis: {
                fontSize: 38,
                ...commonStyle
            },
            smallEmphasis: {
                ...commonStyle
            },
            small: {
                fontSize: 17,
                opacity: 0.5,
                ...commonStyle
            }
        }

        return(
            <div style={divStyle}>
                <LightningCounter />
            </div>
        )
    }
}

ReactDOM.render(
    <LightningCounterDisplay />,
    document.querySelector('#container')
);
```

## 카운터 켜기
- ```setInterval```함수를 사용해 1초마다 100만큼 값을 증가시키는 코드를 호출하기
- ```componentDidMount``` : 이 메소드는 컴포넌트가 렌더링(또는 마운트)된 후에 실행된다.
- ```setState``` : 이 메소드는 state 객체의 값을 갱신할 수 있게 해준다.

### 초기 상태 값 설정
- ```LightningCounter``` 컴포넌트 생성자 안에 ```state```객체를 지정했는데, 이는 컴포넌트가 렌더링되기 전에 실행되게 하기 위함이다.
- 즉, 0으로 초기화된 ```strikes```속성을 담은 객체를 준비하라는 지시
``` js
class LightningCounter extends React.Component {
    render(){
        constructor(props) {
          super(props);
          
          this.state = {
            strikes: 0 // 카운터 역할을 할 변수
          };
        }
        return(
            <h1>{this.state.strikes}</h1> // strikes 속성을 시각화.
        );
    }
}
```
### 타이머 가동과 상태 설정
- ```componentDidMout``` 메소드 추가
- 이 메소드는 컴포넌트가 렌더링 된 후에 한번 호출 됨
- 그 안에 매초마다 ```timerTick```함수를 호출하는 ```setInterval```메소드를 추가함
- ```timerTick```함수는 단지 ```setState```를 호출할 뿐.
- ```setState``` 메소드는 여러 형태로 사용할 수 있는데 여기서는 객체 하나를 인자로 받게 했다. 이 객체에는 ```state```객체로 병합시키기 원하는 모든 속성을 넣을 수 있고, 여기서는 현재 값에 100을 더한 값으로 설정한 ```strikes```속성을 넣었다.
- ```timerTick``` 콘첸츠에 컴포넌트의 컨텍스트가 유지 되기 않기 때문에 명시적으로 바인딩을 해야한다.(TypeError 오류남)
- ```this.timerTick = this.timerTick.bind(this);```
``` js
class LightningCounter extends React.Component {
    render(){
        constructor(props) {
          super(props);
          
          this.state = {
            strikes: 0 // 카운터 역할을 할 변수
          };
          
          this.timerTick = this.timerTick.bind(this);
        }
        
        componentDidMout(){
          setInterval(this.timerTick, 1000);
        }
        
        timerTick(){
          this.setState({
            strikes: this.state.strikes + 100
          })
        }
        
        return(
            <h1>{this.state.strikes}</h1> // strikes 속성을 시각화.
        );
    }
}
```

### 상태 변경 후 렌더링
- ```setState```를 통해 ```state```객체에 어떤 내용이 변경될 때마다 컴포넌트의 ```render```메소드가 자동으로 호출된다.
- 이는 다시 연관된 다른 모든 컴포넌트들의 ```render``` 함수를 연쇄적으로 호출하며, UI의 최종적인 상태가 화면에 보이게 된다.

## 전체코드
``` js
class LightningCounter extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            strikes: 0
        };

        this.timerTick = this.timerTick.bind(this);
    }

    timerTick() {
        this.setState({
            strikes: this.state.strikes + 100
        });
    }

    componentDidMount() {
        setInterval(this.timerTick, 1000);
    }

    render(){
        var counterStyle = {
            fontSize: 50,
            color: "#66ffff"
        };

        var count = this.state.strikes.toLocaleString();

        return(
            <h1 style={counterStyle}>{this.state.strikes}</h1>
        );
    }
}
class LightningCounterDisplay extends React.Component {
    render(){
        var commonStyle = {
            margin: 0,
            padding: 0
        };

        var divStyle = {
            width: 250,
            padding: 40,
            backgroundColor: '#020202',
            borderRadius: 10,
            textAlign: 'center',
            fontFamily: 'sans-serif',
            color: '#999'
        };

        var textStyle = {
            emphasis: {
                fontSize: 38,
                ...commonStyle
            },
            smallEmphasis: {
                ...commonStyle
            },
            small: {
                fontSize: 17,
                opacity: 0.5,
                ...commonStyle
            }
        }

        return(
            <div style={divStyle}>
                <LightningCounter />
                <h2 style={textStyle.smallEmphasis}>LIGHTNING STRIKES</h2>
                <h2 style={textStyle.emphasis}>WORLDWIDE</h2>
                <p style={textStyle.small}>(since you loaded this example)</p>
            </div>
        )
    }
}

ReactDOM.render(
    <LightningCounterDisplay />,
    document.querySelector('#container')
);
```


#### 왜 constructor를 명시해야하는가?
```state```의 값을 초기화 시키기 위함과 초기의 값으로 값들을 세팅하기 위해서.
- 어떠한 ```component```가 실행될 때 ```render()``` 함수보다 먼저 실행이 되면서 그 컴포넌트를 초기화 시켜주고 싶은 ```코드들```을 ```constructor``` 안에다가 코드를 작성

#### 왜 super(props)를 명시해줘야하는가?
- ```constructor``` 사이클이 끝나기 전 ```this.props```가 생성되는 것을 보장함.
- 자바스크립트에서는 ```super```는 부모 클래스 생성자를 가리킨다. (리액트에서는 ```React.Component```)
- 중요한것은, ```super(props)``` 선언전까지 ```constructor```에서 ```this```키워드를 사용할 수 없다.
- ```super(props)```를 호출 한 이유는 컴포넌트를 만들게 되면서 Component를 상속했으며, constructor를 작성하게 되면
기존의 클래스 생성자를 덮어쓰게 된다. 그렇기에 리액트 컴포넌트가 지니고 있던 생성자를 super를 통해 미리 실행하고 그다음에 
우리가 할 작업(state 설정)을 해 주는 것이다.

``` js
class LightningCounter extends React.Component {
    render(){
        // Class Fields 문법
        state = {
          strikes: 0
        }
        
        // Constructor 에서 설정
        constructor(props) {
          super(props);
          //-> 여기서부터 this 사용 가능
          this.state = {
            strikes: 1
          };
        }
        // ...
    }
}
```


### .
### .
### .
### (2020.02.04 내용추가)
- ```state``` : props의 값에 따라서 내부 구현에 필요한 데이터들
- ```props``` : 사용자가 컴포넌트를 사용하는 입장에서 중요한 것.
즉, Component에서 Props(외부)를 통해 사용자가 조작하면 State(내부)에서 데이터 가공(?)



