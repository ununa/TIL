# ES2015 Symbol & Number 타입
ES2015에서 부터 정수 리터럴을 이용해 8진수와 2진수를 표현할 수 있게 되었다.

## 숫자
- 기존 JavaScript에서는 10진수와 16진수의 표현만 가능했었음
- ES2015에서는 2진수와 8진수를 표현하는 정수 리터럴 표기법이 추가됨
- 8진수를 사용하기 위해선 숫자 앞에 0을 붙였지만,
- ES2015에서 부터는 명확하게 ```0o```를 숫자앞에 붙이는 것으로 8진수를 사용할 수 있음
``` js
// 8진수(Octal) - 숫자 앞에 0o을 붙여서 표기
> 0o123
83

// 2진수(Binary) - 숫자 앞에 0b을 붙여서 표기
> 0b101
5
```

## Symbol
- Symbol은 ECMAScript 2015 부터 추가된 원시 자료형의 하나
- 고유하고 변경할 수 없는 값을 정의하는데 사용됨.
- 이러한 특성을 이용해서 객체의 프로퍼티 식별자로도 사용함
``` js
// 1.
const foo = Symbol();
const bar = Symbol();

console.log(foo === bar);  //-> false
console.log(typeof foo);  //-> Symbol

// 2.
const alice = Symbol("Alice");
console.log(alice);  //-> Symbol(Alice)
```
- ```Symbol()```을 호출하여 생성한 값은 모두 유일한 값이 된다.
- ```typeof```연산자를 사용해 심볼의 데이터 타입을 확인 할 수 있다.
- 심볼을 생성할 때 ```Symbol()```에 인수를 전달하여 설명을 추가할 수 있다.
