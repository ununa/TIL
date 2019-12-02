# ES6 Object에 추가된 기능
## 프로퍼티 단축 구문
객체의 프로퍼티를 단순하게 표기할 수 있음.
``` js
let name = "Alice";
let age = 10;

// 기존 ES5 표기법
var alice = {
  name: name,
  age: age
}

// ES6 표기법
let alice = { name, age };
console.log(alice); // { name: 'Alice', age: 10 }
```

## 계산된 프로퍼티 이름(Computed Property names)
- 객체의 프로퍼티 이름에 평가값을 사용할 수 있게 됨
- 프로퍼티 이름에 대괄호를 이용해 평가식으로 사용할 수 있으며,
- 평가된 값이 문자열 타입으로 전환되어 프로퍼티명으로 사용됨.
``` js
let name = "myName";
let num = 1;

// 대괄호를 이용해 평가식으로 사용한 방법
let person = {
  [ name + num ]: "alice"
}
console.log(person); // { myName1: 'alice' }

// 객체의 프로퍼티 명으로 심볼을 사용할 수 있으며,
// 심볼이 사용되었다면 심볼을 프로퍼티명으로 사용됨
let person = {
  [ Symbol("name) ]: "Alice"
}

console.log(person); // { [Symbol(name)]: 'Alice' }
```

## 메서드 단축 구문
- 객체의 메서드를 정의할 때 기존의 함수 리터럴 표기법보다 간략한 표기법을 사용할 수 있음
- 단, ```method() {}``` 메서드 표기법은 객체의 메서드로만 사용할 수 있고, 객체 생성자 함수로는 사용할 수 없음.
``` js
// 기존 ES5 표기법
var alice = {
  intoTheRabbitHole: function() {
    console.log('Rabbit Hole')
  }
}

// ES6 표기법
var alice = {
  intoTheRabbitHole() {
    console.log('Rabbit Hole');
  }
}
```
