
- - -

## 03. 화살표 함수
ES6에서 도입된 새로운 피처. 
``` javascript
// regular function
const testFunction = function() {
  // content..
}

// arrow function
const testFunction = () => {
  // content..
}
```

### 기존 함수 선언 방법에서 화살표 함수 선언 방법으로 바꾸는 단계
1. function 키워드 지우기
2. ()다음에 뚱뚱한 화살표(fat arrow, =>) 기호 넣기

괄호는 기존 함수 선언 방식에서와 마찬가지로 매개변수를 감싸는 용도로 사용된다. 만약 매개 변수가 하나라면 괄호를 생략할 수 있다.
``` javascript
const testFunction = (firstName, lastName) => {
  return firstName+' '+lastName;
}

const singleParam = firstName => {
  return firstName;
}
```

### 암묵적 반환(Implicit return)
화살표 함수의 본문(body)이 한 줄로만 구성되었다면, 반환 값 앞에 ```return```키워드를 생략할 수 있다.  
몸체를 감싸는 중괄호 ```{}``` 역시 생략 가능하다.
``` javascript
const testFunction = () => 'hello there.';
testFunction(); 
```

### React에서 어떻게 쓰이나?
React 컴포넌트를 만들 때 화살표 함수를 쓸 수 있다.
``` javascript
const HelloWorld = (props) => {
  return <h1>{props.hello}</h1>;
}
```
화살표 함수를 써서 만든 react 컴포넌트는 ES6 클래스 컴포넌트와 동일하다.
``` javascript
class HelloWorld extends Component {
  render() {
    return (
      <h1>{props.hello}</h1>;
    );
  }
}
```
! 화살표 함수는 코드를 좀 더 간결하게 만들어 주지만 간견해진 대신 컴포넌트에서 라이프사이클을 활용하지 못하는 단점이 있다.  
이런 종류의 컴포넌트는 stateless 함수형 컴포넌트(functional component)라 불리운다.






