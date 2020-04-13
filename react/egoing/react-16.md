# React - 6. 이벤트

### 이벤트 state props 그리고 render 함수
- React에선 Props의 값이나 State값이 바뀌면 render 함수가 다시 호출된다.

### 이벤트 설치
#### App.js
``` js
return (
  <div className="App">
    <header>
        <h1><a href="/" onClick={function(e){
          console.log(e);
          e.preventDefault();
        }}>{this.state.subject.title}</a></h1>
        <p>{this.state.subject.sub}</p>
    </header>
    <TOC data={this.state.contents}></TOC>
    <Content title={_title} desc={_desc}></Content>
  </div>
);
```

### 이벤트에서 state 변경하기
- ```bind```
- ```setState```

### 이벤트에서 bind 함수 이해하기
``` js
var obj = {name: 'egoing'};
function bindTest(){
  console.log(this.name);
}
var bindTest2 = bindTest.bind(obj);
bindTest2();
```
- render 함수가 호출될 때 this는 컴포넌트 자체를 가리킨다.
- bind 함수로 인해서 bindTest함수에 this는 object가 된다.
- 새로운 함수가 복제가 되어 만들어진다.

### 이벤트 setState 함수 이해하기










### 설치 후 순서
- ```create react app . ``` : 현재 폴더에 react 개발환경 구축
- ```npm run start``` : 실행
- ```npm run build``` : 배포
- ```npm install -g serve```
- ```npx serve -s build```

### 컴포넌트 만들기
``` js
class Subject extends Component {
  render() {
    return(
      <header>
        <h1>WEB</h1>
        <p>World Wide Web!</p>
      </header>
    )
  }
}

class App extends Component {
  render() {
    return (
      <div className="App">
        <Subject></Subject>
      </div>
    );
  }
}
```
- Component의 내부는 하나의 최상위 태그로 시작되어야 한다.


### props
#### Refactoring
``` js 
class Subject extends Component {
  render() {
    return(
      <header>
        <h1>{this.props.title}</h1>
        <p>{this.props.sub}</p>
      </header>
    )
  }
}

class App extends Component {
  render() {
    return (
      <div className="App">
        <Subject title="WEB" sub="World Wide Web!"></Subject>
      </div>
    );
  }
}
```

### State
``` js
class App extends Component {
  constructor(props){
    super(props);
    this.state = {
      subject: {title:'WEB', sub:'World Wide Web!'}
    }
  }

  render() {
    return (
      <div className="App">
        <Subject
          title={this.state.subject.title}
          sub={this.state.subject.sub}>
        </Subject>
        <TOC></TOC>
        <Content title="HTML" desc="HTML is HyperText Markup Language."></Content>
      </div>
    );
  }
}
```
- Props: 사용자의 입장
- State: 내부적 구현에 필요한 데이터들
- Props와 State가 분리되어 있어야 한다.
- 컴포넌트가 실행될 때 rener라고 하는 함수보다 먼저 실행이 되면서 그 컴포넌트를 초기화 시켜주고 싶은 코드는 constructor 안에 코드를 작성한다.
- 초기화가 끝나면 this.state = {}
- 상위 컴포넌트인 App의 상태를 하위 컴포넌트로 전달하고 싶을때는 상위 컴포넌트의 state 값은 하위 컴포넌트의 props의 값으로 전달하는건 얼마든지 가능하다.
- 부모인 입장에서는 state라는 내부 정보를 사용했고, 자식에게 전달할 때는 props를 통해 전달한다. 

### key
- React가 내부적으로 어떤 항목을 변경, 추가 또는 삭제할지 식별하는 것들 돕는다. 
- 추가링크: https://ko.reactjs.org/docs/lists-and-keys.html