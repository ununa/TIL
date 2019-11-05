## 05. 함수
특정 코드를 하나의 명령으로 실행 할 수 있게 해주는 기능.
``` js
const a = 1;
const b = 2;
const sum = a + b;
```
를 함수로 만들면 
``` js
function add(a, b) {
  return a + b;
}

const sum = add(1, 2);
console.log(sumb) // 3
```
함수를 만들 때 ```function```키워드를 사용하며, 함수에서 어떤 값을 받아올지 정해주는 것을 파라미터(매개변수)라고 부른다.
함수 내부에서 ```return```키워드를 사용하여 함수의 결과물을 지정 할 수 있으며, ```return```을 하게 되면 함수가 끝나며, 아래 코드들은 실행이 안된다.

#### 잠깐! 템플릿 리터럴
``` js
function hello(name) {
  console.log(`Hello, ${name}!`);
}
hello('velopert');
```

### 화살표 함수
``` js
const add = (a, b) => {
  return a + b;
};

console.log(add(1, 2));

// 화살표 함수 줄여서 쓰는 방법.
const add = (a, b) => a + b;
console.log(add(1, 2));
```
```function```키워드 대신에 => 문자를 사용해서 함수를 구현.  
화살표의 좌측에는 함수의 파라미터, 화살표 우측에는 코드 블록이 들어감.

단, 일반 ```function```으로 만든 함수와 화살표 함수에서 가르치는 this가 서로 다름.
