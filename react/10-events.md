# 이벤트

## 이벤트 리스닝하기와 반응하기
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
        
        this.increase = this.increase.bind(this); << 추가
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
                <button onClick={this.increase} style={buttonStyle}>+</button> << 속성추가
            </div>
        );
    }
}
```

## 이벤트 속성
### 합성 이벤트
리액트는 JSX에 이벤트를 지정하는 경우, DOM이벤트를 직접 다루지 않는다. ```SyntheticEvent```는 리액트의 특별한 이벤트 유형인데, ```MouseEvent```나 ```KeyboardEvent``` 등과 같은 네이티브 이벤트 타입을 받지 않고 이벤트를 래핑하는 ```SyntheticEvent``` 타입을 인자로 받는다.


