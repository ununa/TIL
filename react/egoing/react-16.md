# React - 6. 이벤트

### 이벤트 state props 그리고 render 함수
React에선 Props의 값이나 State값이 바뀌면 render 함수가 다시 호출된다.

### 이벤트 설치
#### [App.js]
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
#### tip! debugger*

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
- 변경하고 싶은 값을 객체의 형태로 주어야한다.
- state의 값이 바뀌면 setState로 바꿔야한다.

### 컴포넌트 이벤트 만들기 1
- onChangePage: 이벤트에 설치한 함수를 호출하도록 만드려고 하는 것
- <Subject/>라고 하는 컴포넌트에 onChagePage라는 이벤트를 만들었고, 그 이벤트에 함수를 설치해주면 이벤트가 발생되었을 때 props로 전달된 onChangePage 함수를 호출하면 된다.





