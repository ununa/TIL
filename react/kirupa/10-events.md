# 이벤트

### 이벤트 리스닝하기와 반응하기
버튼을 누를 때 마다 숫자가 증가하는 간단한 카운터를 만들어보자.
1. 플러스 버튼을 누를 때마다 카운터의 값은 1씩 증가한다.
2. 사용자가 버튼을 클릭하면 이벤트가 발생하고, 
3. 이벤트를 리스닝하고 있던 앱은 그 이벤트를 감지해 그에 반응하는 작업을 한다.

### 시작지점
``` js
class Counter extends React.Component {
    render(){
        var textStyle = {
            fontSize: 72,
            fontWeight: 'bold',
            fontFamily: 'sans-serif',
            color: '#333'
        };

        return(
            <div style={textStyle}>
                {this.props.display}
            </div>
        );
    }
}

class CounterParent extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            count: 0
        };
    }

    render(){
        var backgroundStyle = {
            width: 250,
            height: 100,
            padding: 50,
            borderRadius: 10,
            backgroundColor: '#ffc53a',
            textAlign: 'center'
        };
        
        var buttonStyle = {
            width: 30,
            height: 30,
            fontSize: '1em',
            fontFamily: 'sans-serif',
            color: '#333',
            fontWeight: 'bold',
            lineHeight: '3px'
        };

        return(
            <div style={backgroundStyle}>
                <Counter display={this.state.count} />
                <button style={buttonStyle}>+</button>
            </div>
        );
    }
}

ReactDOM.render(
    <div>
        <CounterParent />
    </div>,
    document.querySelector('#container')
);
```

## 버튼 작동시키
플러스 버튼을 클릭할 때마다 카운터의 값이 1씩 증가되게 해야한다.
1. 버튼의 클릭 이벤트를 리스닝한다.
2. 클릭에 반응해 카운터가 의존하는 ```this.state.count``` 속성의 값을 증가시킬 이벤트 핸드러를 구현한다.

>- 리액트에서는 모든 사항을 JSX 자체에 인라인으로 지정하는 방식으로 이벤트를 리스닝한다.
>- 리스닝할 이벤트와 호출될 이벤트 핸들러 모두를 마크업 안에 지정해야 한다.
>- 그렇게 하기 위해 ```CounterParent``` 컴포넌트 안의 ```return``` 함수를 찾아서 수정하자.

3. ```increase``` 함수는 이벤트를 인자로 받고, 이벤트 인자는 e로 접근할 수 있게 지정하였다.
4. 생성자에서는 this를 increase함수에 바인딩 함.

``` js
        return(
            <div style={backgroundStyle}>
                <Counter display={this.state.count} />
                <button onClick={this.increase} style={buttonStyle}>+</button>
            </div>
        );
```
3. onClick 이벤트가 발생하면 increase 함수를 호출

``` js
class CounterParent extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            count: 0
        };
        
        this.increase = this.increase.bind(this); // 추가
    }
    
    // 함수추가
    increase(e) {
        this.setState({
            count: this.state.count + 1
        });
    }

    render(){
        var backgroundStyle = {
            width: 250,
            height: 100,
            padding: 50,
            borderRadius: 10,
            backgroundColor: '#ffc53a',
            textAlign: 'center'
        };
        
        var buttonStyle = {
            width: 30,
            height: 30,
            fontSize: '1em',
            fontFamily: 'sans-serif',
            color: '#333',
            fontWeight: 'bold',
            lineHeight: '3px'
        };

        return(
            <div style={backgroundStyle}>
                <Counter display={this.state.count} />
                <button onClick={this.increase} style={buttonStyle}>+</button> // 속성추가
            </div>
        );
    }
}
```

## 이벤트 속성
### 합성 이벤트
- 리액트는 JSX에 이벤트를 지정하는 경우, DOM이벤트를 직접 다루지 않는다.
- ```SyntheticEvent```는 리액트의 특별한 이벤트 유형인데, ```MouseEvent```나 ```KeyboardEvent``` 등과 같은 네이티브 이벤트 타입을 받지 않고 이벤트를 래핑하는 ```SyntheticEvent``` 타입을 인자로 받는다.
- 합성 이벤트와 그 속성을 사용할 때는 리액트의 ```SyntheticEvent```문서 참고하자.

* ```SyntheticEvent``` 속성
    - ```boolean bubbles```
    - ```boolean cancelable```
    - ```DOMEventTarget currentTarget```
    - ```boolean defaultPrevented```
    - ```number eventPhase```
    - ```boolean isTrusted```
    - ```DOMEvent nativeEvent```
    - ```void preventDefault()```
    - ```boolean isDefaultPrevented()```
    - ```void stopPropagation()```
    - ```boolean isPropagationStopped()```
    - ```DOMEventTarget target```
    - ```number timeStamp```
    - ```string type```

### 이벤트 속성 다루기
- 플러스 버튼을 누를 때 1씩 증가하는 카운터
- 키보드의 ```Shift키```를 누른 채로 플러스 버튼을 클릭하면 카운터가 10씩 증가
``` js
    increase(e) {
        var currentCount = this.state.count;
        if(e.shiftKey) { // SyntheticEvent 인자
            currentCount += 10;
        } else {
            currentCount += 1;
        }
        this.setState({
            count: currentCount
        });
    }
```

## 또 다른 이벤트 처리 기법
### 컴포넌트의 이벤트는 직접 리스닝 할 수 없다.
- 컴포넌트는 DOM 이벤트를 감싸는 래퍼이다. 
- 이벤트 핸들러를 속성처럼 다루고 컴포넌트에 전달할 수 있는 차선책이 있다. 바로 컴포넌트 안에서 DOM 엘리먼트에 이벤트를 할당하고 속성의 값으로 이벤트 핸들러를 설정하면 된다.
- 런타임 시에 ```clickHandler``` 속성은 ```increase``` 함수로 평가되며, 플러스 버튼을 클릭했을 때 ```increase``` 함수의 호출이 보장된다.
``` js
// 컴포넌트 추가
class PlusButton extends React.Component {
    render() {
        return (
            <button onClick={this.props.clickHandler}> // onClick 이벤트 추가하고 값으로 clickHandler 속성 지정
                +
            </button>
        )
    }
}

class CounterParent extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            count: 0
        };
        
        this.increase = this.increase.bind(this);
    }
    
    increase(e) {
        this.setState({
            count: this.state.count + 1
        });
    }

    render(){
        var backgroundStyle = {
            width: 250,
            height: 100,
            padding: 50,
            borderRadius: 10,
            backgroundColor: '#ffc53a',
            textAlign: 'center'
        };
        
        var buttonStyle = {
            width: 30,
            height: 30,
            fontSize: '1em',
            fontFamily: 'sans-serif',
            color: '#333',
            fontWeight: 'bold',
            lineHeight: '3px'
        };

        return(
            <div style={backgroundStyle}>
                <Counter display={this.state.count} />
                <PlusButton clickHandler={this.increase} /> // clickHandler 속성 추가
            </div>
        );
    }
}
```

### 일반 DOM 이벤트의 리스닝
``` js
class Something extends React.Component {
    .
    .
    .
    handleMyEvent(e) {
        // 이벤트 처리
    }
    
    render() {
        return(
            <div onSomeEvent={this.handleMyEvent}>Hello!</div> 
        );
    }
}
```
- 이 방법으로는 코드가 작동하지 않음
- 리액트가 인식할 수 있는 공식 이벤트가 아니기 때문이다.
- 이 경우에는 컴포넌트 생명주기 메소드에서 ```addEventListener```를 사용해야한다.

``` js
    componentDidMount() {
        window.addEventListener('someEvent', this.handleMyEvent);
    }
    
    componentWillUnmount() {
        window.removeEventLister('someEvent', this.handleMyEvent);
    }
```
- ```Something```은 ```someEvent```라는 이벤트를 리스닝 하는 컴포넌트다.
- 컴포넌트가 렌더링 되면 자동으로 호출되는 ```componentDidMount``` 메소드에서 ```someEvent```의 리스닝을 시작한다.
- 이때 ```addEventListener```에 이벤트와 이벤트 핸들러를 전달하는 방식이 사용된다.
- ★ 단, 컴포넌트가 소멸될 때 이벤트 리스너도 제거해야한다.
- ```componentDidMount``` 메소드와 대응 관계인 ```componentWillUnmount``` 메소드를 이용하면 되는데, 즉 ```componentWillUnmount``` 메소드 안에 ```removeEventListener``` 함수를 추가함으로써, 컴포넌트가 소멸된 후에는 더 이상 이벤트 리스닝을 하지 않는다.

### 이벤트 핸들러 내부의 this
리액트에서 이벤트 핸들러 내부의 ```this```는 DOM의 경우와 다른데, 리액트에선 이벤트를 발생시킨 엘리먼트의 참조가 아니며, 그 값은 도움이 안 되는, 그냥 ```undefined```이다. 그래서 bind 메소드를 사용해 ```this```를 명시적으로 지정해야한다.
``` js
class PlusButton extends React.Component {
    render() {
        return (
            <button onClick={this.props.clickHandler}>
                +
            </button>
        )
    }
}

class CounterParent extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            count: 0
        };
        
        this.increase = this.increase.bind(this); // CounterParent 컴포넌트를 참조한다. this의 값을 컴포넌트에 바인딩 시켰기 때문.
    }
    
    increase(e) {
        this.setState({
            count: this.state.count + 1
        });
    }

    render(){
        var backgroundStyle = {
            width: 250,
            height: 100,
            padding: 50,
            borderRadius: 10,
            backgroundColor: '#ffc53a',
            textAlign: 'center'
        };
        
        var buttonStyle = {
            width: 30,
            height: 30,
            fontSize: '1em',
            fontFamily: 'sans-serif',
            color: '#333',
            fontWeight: 'bold',
            lineHeight: '3px'
        };

        return(
            <div style={backgroundStyle}>
                <Counter display={this.state.count} />
                <PlusButton clickHandler={this.increase} />
            </div>
        );
    }
}
```
