
## 03. 연산자

### 산술 연산자
산술 연산자는 사칙연산과 같은 작업을 하는 연산자를 의미
- ```+``` : 덧셈
- ```-``` : 뺄셈
- ```*``` : 곱셈
- ```/``` : 나눗셈

``` js
let a = 1;
console.log(a++);
console.log(++a);
```

```console.log(a++);``` 를 할 때에는 1을 더하기 직전 값을 보여주고  
```console.log(++a);``` 를 할 때에는 1을 더한 다음의 값을 보여줌

### 대입 연산자
대입 연산자는 특정 값에 연산을 한 값을 바로 설정 할 때 사용 할 수 있는 연산자
``` js
let value = 1; // 변수 선언
value = 2; // 대입 연산자
```
:point_up: 단, 첫번째 줄은 새로운 변수를 선언하는 것으로서, 대입 연산자에 해당하지 않는다.

``` js
let a = 1;
a = a + 3;
```

위 코드를 대입 연산자를 사용하면 
``` js
let a = 1;
a += 3;
```
이 외에도
``` js
let a = 1;
a += 3; // 4
a -= 3; // 1
a *= 3; // 4
a /= 3; // 1
console.log(a); // 결과는 1이 나타나게 된다.
```

### 논리 연산자
불리언 타입 (true 혹은 false)를 위한 연산자
- ```!```: NOT
- ```&&```: AND
- ```||```: OR

#### NOT
true는 false로, false는 true로 바꿔줌.
``` js
const a = !true; // a = false
const b = !false; // b = true
```

#### AND
양쪽의 값이 둘 다 true 일때만 true.
``` js
const a = true && true; // a = true

// f 모두 false.
let f = false && false;
f = false && true;
f = true && false;
```

#### OR
양쪽의 값 중 하나라도 true라면 결과물이 true.  
두 값이 둘 다 false 일 때에만 false.
``` js
// 모두 true.
let t = true || false;
t = false || true;
t = true || true;

// f는 false.
let f = false || false;
```


### 연산 순서
```NOT``` -> ```AND``` -> ```OR``` 
``` js
const value = !((true && false) || (true && false) || !false); // !true; = false.
```

### 비교 연산자
두 값을 비교 할 때 사용

#### 두 값이 일치하는지 확인
```js
const a = 1;
const b = 1;
const equals = a === b;
console.log(equals); // true.
```
```==```와 ```===```의 차이점은 타입 검사 여부인데 예를들어 ```==```를 사용하면
숫자 1과 문자 '1'이 동일한 값으로 간주되기 때문에 ```===```를 사용 할 것.
```js
const a = 1;
const b = '1';
const equals = a == b;
console.log(equals); // true

const a = 0;
const b = false;
const equals = a == b;
console.log(equals); // true

const a = null;
const b = undefined;
const equals = a == b;
console.log(equals); // true
```

#### 두 값이 일치하지 않는지 확인
```js
const value = 'a' !== 'b';
```
이도 역시 ```!=``` 보다 ```!==``` 사용을 권장함.

#### 크고 작음
```js
const a = 10;
const b = 15;
const c = 15;

console.log(a < b); // true
console.log(b > a); // true
console.log(b >= c); // true
console.log(a <= c); // true
console.log(b < c); // false;
```
