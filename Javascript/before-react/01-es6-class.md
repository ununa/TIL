# React를 배우기 전에 알아야 할 자바스크립트 기초

### React를 학습하기 위해 알아야 할 자바스크립트 피처 리스트
- [ES6 classes](https://dev.to/nsebhastian/javascript-basics-before-you-learn-react-38en#es6-classes)
- [The new variable declaration let/const](https://dev.to/nsebhastian/javascript-basics-before-you-learn-react-38en#declaring-variables-with-es6-let-and-const)
- [Arrow functions](https://dev.to/nsebhastian/javascript-basics-before-you-learn-react-38en#the-arrow-function)
- [Destructuring assignment](https://dev.to/nsebhastian/javascript-basics-before-you-learn-react-38en#destructuring-assignment-for-arrays-and-objects)
- [Map and filter](https://dev.to/nsebhastian/javascript-basics-before-you-learn-react-38en#map-and-filter)
- [ES6 module system](https://dev.to/nsebhastian/javascript-basics-before-you-learn-react-38en#es6-module-system)


## 00. Create React App 탐험하기
``` javascript
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a
            className="App-link"
            href="https://reactjs.org"
            target="_blank"
            rel="noopener noreferrer"
          >
            Learn React
          </a>
        </header>
      </div>
    );
  }
}

export default App;
```

## 01. ES6 클래스
ES6에선 자바나 파이썬 같은 객체지향언어에서 쓰이는 클래스가 도입됨.

``` javascript
class Developer {
  constructor(name){
    this.name = name;
  }

  hello(){
    return 'Hello World! I am ' + this.name + ' and I am a web developer';
  }
}
```
- ```class```는 새로운 객체를 생성할 때 쓰이는 식별자(또는 간단한 이름, 위 코드에선 Developer)앞에 쓰인다.  
- ```생성자(constructor)```메서드는 객체를 초기화 할 때 호출된다.  
- 생성자에 전달되는 매개변수는 새로 만들어지는 객체에 전달 된다.  
- 클래스엔 원하는 만큼의 메서드를 정의할 수 있다.

### 클래스 상속
클래스는 다른 클래스의 정의를 ```extends(확장)``` 할 수 있으며, 확장한 클래스로 만든 객체엔
기존 클래스와 확장한 클래스에서 정의한 모든 메서드가 있다.

``` javascript
class ReactDeveloper extends Developer {
  installReact(){
    return 'installing React .. Done.';
  }
}

var nathan = new ReactDeveloper('Nathan');
nathan.hello(); // Hello World! I am Nathan and I am a web developer
nathan.installReact(); // installing React .. Done.
```
- 다른 클래스를 ```extends(확장)```해서 만든 클래스는 ***자식 클래스(child class)*** 혹은 ***서브 클래스(sub class)*** 라고 브른다.
- 피 확장 클래스는 ***부모 클래스(parent class)*** 혹은 ***슈퍼 클래스(super class)***라고 브른다.
- 자식 클래스는 부모 클래스에 정의된 메서드를 ***오버라이드(override)*** 할 수 있는데, 이는 부모 클래스에 정의된 메서드를 자식 클래스에서 새롭게 정의하고 교체한다는 의미이다.

#### 자식 클래스 ReactDeveloper에서 부모 클래스(Developer)의 함수, hello를 오버라이드 해보기.
``` javascript
class ReactDeveloper extends Developer {
  installReact(){
    return 'installing React .. Done.';
  }
  
  hello(){
    return 'Hello World! I am ' + this.name + ' and I am a REACT developer';
  }
}

var nathan = new ReactDeveloper('Nathan');
nathan.hello(); // Hello World! I am Nathan and I am a REACT developer
// Developer 클래스에서 정의했던 hello 메서드가 오버라이드되어 새로운 문자열이 반환됨
```

### React에서 어떻게 쓰이나?
지금까지 ES6의 클래스와 상속에 관한 개념을 학습한 것이며, 맨 상단에 있는 ```src/app.js```에 쓰인 React 클래스는 React 컴포넌트(component)라는 걸 알 수 있다.
이 컴포넌트는 단순히 React 패키지로부터 import한 React 컴포넌트 클래스를 상속받은 평범한 ES6 클래스 일 뿐이다.
``` javascript
import React, { Component } from 'react';

class App extends Component {
  // class content
  render(){
    return (
      <h1>Hello React!</h1>
    )
  }
}
```
이렇게 (React) 컴포넌트 클래스를 상속받았고, ```Component``` 클래스에 정의 되어 있기 때문에 ```render()``` 메서드, JSX, ```this.state``` 등의 다양한 메서드를 사용할 수 있게 됨.  
만약 상태(state)나 라이프사이클과 관련된 메서드(lifecycle method)가 필요하지 않다면, 함수를 대신 사용할 수도 있음

- - -






