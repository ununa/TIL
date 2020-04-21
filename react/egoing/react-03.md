# React - 3. 개발환경

### npm을 이용해서 create react app 설치

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
- Component는 HTML을 반환하는 함수이다.
- 리액트에서는 한번에 하나의 컴포넌트만 렌더링 할 수 있다.



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
nomade coder
- props는 자식 컴포넌트로 값을 보내준다.
- props는 객체 형태로 자식 컴포넌트에게 넘어가며, 자식 컴포넌트에서는 파라미터로 props를 받고, 객체의 요소를 사용하는 것과 동일하게 props 값들을 사용할 수 있다.
- ES6에서 지원하는 구조분해 문법도 알아보자.



### key
- React가 내부적으로 어떤 항목을 변경, 추가 또는 삭제할지 식별하는 것들 돕는다. 
- 추가링크: https://ko.reactjs.org/docs/lists-and-keys.html