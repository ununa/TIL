# 컴포넌트 생명주기
컴포넌트는 속성, 상태, 이벤트를 다룰 때 도움을 주며, 종종 다른 컴포넌트의 안녕에 대해서도 책음을 진다. 따라서 컴포넌트가 하는 모든 일을 추적하는 작업은 쉬지 않은데,  
이를 위해 리액트는 생며웆기 메소드(lifecyle method)를 제공한다.

## 생명주기 메소드와의 만남
- componentWillMount
- componentDidMount
- componentWillUnmount
- componentWillUpdate
- componentDidUpdate
- shouldComponentUpdate
- componentWillReceiveProps
- componentDidCatch

이게 전부가 아니지만, 생명주기 메소드와 함께 자주 사용할 하나의 메소드는  바로 ```render```메소드 이다.

## 생명주기 메소드의 작동 확인
예제링크: https://www.kirupa.com/react/lifecycle_example.htm
1. 생명주기 메소드로 시작되었으며
2. 플러스 버튼을 누를 때 마다 생명주기 메소드 메세지가 호출된다.
3. 마지막으로 카운터의 값이 5가 되면 이 카운터는 콘솔에 메세지를 남기고 사라지게 된다.
4. 이 때가 예제의 마지막에 도달한 시점이며, 페이지를 리프레시 하면 다시 처음부터 시작할 수 있다.

```js
  var destination = document.querySelector("#container");

  class Counter extends React.Component {
    render() {
      var textStyle = {
        fontSize: 72,
        fontFamily: "sans-serif",
        color: "#333",
        fontWeight: "bold"
      };

      console.log("render: Counter component");

      return (
        <div style={textStyle}>
          {this.props.display}
        </div>
      );
    }
  }

  class CounterParent extends React.Component {
    constructor(props) {
      super(props);
      console.log("constructor: It's default time!");

      this.state = {
        count: 0
      };
      this.increase = this.increase.bind(this);
    }

    increase() {
      this.setState({
        count: this.state.count + 1
      });
    }

    static getDerivedStateFromProps(props, state) {
      console.log("getDerivedStateFromProps: You probably don't need this!")

      return null;
    }

    componentDidUpdate(currentProps, currentState) {
      console.log("componentDidUpdate: Component just updated!");
    }

    getSnapshotBeforeUpdate(prevProps, prevState) {
      console.log("getSnapshotBeforeUpdate: Component is about to commit its changes!")

      return null;
    }

    componentDidMount() {
      console.log("componentDidMount: Component is inserted into the tree!");
    }

    componentWillUnmount() {
      console.log("componentWillUnmount: Component is about to be removed from the DOM!");
    }

    shouldComponentUpdate(newProps, newState) {
      console.log("shouldComponentUpdate: Should component update?");
      if (newState.count < 5) {
        console.log("shouldComponentUpdate: Component should update!");
        return true;
      } else {
        ReactDOM.unmountComponentAtNode(destination);
        console.log("shouldComponentUpdate: Component should not update!");
        return false;
      }
    }

    render() {
      var backgroundStyle = {
        padding: 50,
        border: "#333 2px dotted",
        width: 250,
        height: 100,
        borderRadius: 10,
        textAlign: "center"
      };
      console.log("render: CounterParent component");
      return (
        <div style={backgroundStyle}>
          <Counter display={this.state.count} />
          <button onClick={this.increase}>
            +
          </button>
        </div>
      );
    }
  };

  ReactDOM.render(
    <div>
      <CounterParent />
    </div>,
    destination
  );
```

## 초기 렌더링 단계
```
1. 기본 속성 설정
2. 기본 상태 설정
3. componentWillMount
4. render
5. componentDidMount
```

### 기본 속성 설정
컴포넌트의 ```defaultProps``` 속성은 ```this.props```의 기본값을 지정할 수 있게 해준다.  
CounterParent 컴포넌트의 name 속성을 설졍하려면 다음과 같이 하면 된다.
``` js
CounterParent.defaultProps = {
  name: 'Iron Man'
};
```
이는 컴포넌트가 생성되기 전이나 부모로부터 속성이 전달될 때 실행된다.

### 기본 상태 설정
이 단계는 컴포넌트의 생성자 안에서 진행된다. 따라서 컴포넌트 생성 과정에서 this.state의 기본값을 지정할 수 있는 기회로 삼을 수 있다.
``` js
constructor(props) {
  super(props);
  
  console.log('constructor: Default state time!');
  
  this.state = {
    count: 0
  };
  
  this.increase = this.increase.bind(this);
}
```
여기서는 state 객체를 정의했고, 그 count 속성을 0으로 초기화 했다.

### componentWillMount
컴포넌트가 DOM 안으로 렌더링되기 전에 호출되는 마지막 메소드다. 이 메소드 안에는 setState를 호출해도 컴포넌트가 다시 렌더링 되지 않는 점을 기억하자.

### render
모든 컴포넌트에 정의돼 있어야 하는 메소드이며, JSX를 리턴하는 책임을 진다. 렌더링이 필요 없다면 단순히 null 이나 false를 리턴하면 된다.

### componentDidMount
컴포넌트가 렌더링돼 DOM에 자리 잡은 직후 호출된다. 이 시점에서는 컴포넌트 생성이 완료됐는지 여부를 걱정할 필요 없이 안심하고 DOM쿼리 작업을 수행할 수 있다.  
모든 준비를 마친 컴포넌트에만 의존하는 코드는 모두 이 메소드 안에 지정하면 된다.  
render 메소드를 제외하면 지금까지의 모든 생명주기 메소드들은 한 번만 실행된다. 이는 이후 보게 될 메소드들과 다른 점이다.

## 업데이트 단계
일단 컴포넌트가 DOM 안으로 추가되면, 이후에 속성이나 상태가 변경될 때 업데이트되며 다시 렌더링 된다. 하지만 이 과정에서 또 다른 생명주기 메소드들이 호출된다.

### 상태 변경 다루기
상태가 변경되면 컴포넌트는 render 메소드를 다시 호출한다. 그 컴포넌트의 결과에 의존하는 다른 모든 컴포넌트 역시 자신들의 render 메소드를 호출한다.
```
1. shouldComponentUpdate
2. componentWillUpdate
3. render
4. componentDidUpdate
```

### shouldComponentUpdate
때로는 상태가 변경됐어도 컴포넌트의 업데이트를 바라지 않을 수 없는데, 이 메소드는 그와 같은 업데이트 여부를 제어할 수 있게 해준다.   
만약 true를 리턴하면 컴포넌트는 업데이트되고, false를 리턴하면 업데이트를 건너뛰게 된다.
``` js
shouldComponentUpdate(newProps, newState) {
  console.log('shouldComponentUpdate: Should component update?');
  if (newState.count < 5) {
    console.log('shouldComponentUpdate: Component should update!');
    return true;
  } else {
    ReactDOM.unmountComponentAtNode(destination);
    console.log('shouldComponentUpdate: Component should not update!');
    return false;
  }
}
```
이 메소드는 newPops와 newState라는 두 인자를 받는데, 여기서는 상태 속성인 id의 값이 5보다 작은지 확인한다. 만약 그렇다면 true를 리턴해 컴포넌트가 업데이트돼야 함을 지시하고, id의 값이 5보다 작지 않다면 false를 리턴함으로써 컴포넌트 업데이트를 거부한다.

### componentWillWpdate
이 메소드는 컴포넌트가 업데이트되기 직전에 호출된다. 여기에선 this.setState를 사용해 상태를 변경할 수 없다.

### render
shouldcomponentUpdate가 false를 리턴함으로써 업데이트 작업을 건너뛰지만 않는다면, render 메소드가 다시 호출됨으로써 컴포넌트가 올바로 보이게 보장한다.

### componentDidUpdate
이 메소드는 컴포넌트가 업데이트되고 render 메소드의 실행이 끝난 후에 호출된다. 업데이트 후에 수행하고 싶은 코드가 있다면 이 메소드가 가장 알맞은 장소다.

### 속성 변경 다루기
```
1. componentWillReceiveProps
2. shouldComponentUpdate
3. componentWillUpdate
4. render
5. componentDidUpdate
```
```componentWillReceiveProps```는 하나의 인자를 받는데, 그 인자에는 새로 할당하고자 하는 속성 값이 포함된다.

## 언마운트 단계
컴포넌트가 소멸되고 DOM에서 제거되는 언마운트 단계
```
1. componentWillUnmount
```
오직 하나의 생명주기 메소드가 호출되는데 바로 ```componentWillUnmount```다. 이 메소드에서 이벤트 리스너를 제거하거나 타이머를 중단시키는 등의 뒷정리를 할 수 있고, 이 메소드가 실행된 후에는 컴포넌트는 실제로 DOM으로부터 제거돼 우리와 작별하게 된다.






