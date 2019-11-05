## 00. JS에서의 선언타입
- ```var```
변수를 선언. 추가로 동시에 값을 초기화.

- ```let```
블록 범위(scope) 지역 변수를 선언. 추가로 동시에 값을 초기화.

- ```const```
블록 범위 읽기 전용 상수를 선언.


## 01. 변수와 상수

- **변수** ```var```, ```let```  
바꿀 수 있는 값. 한번 선언하고 나서 바꿀 수 있다.

- **상수** ```const```  
한번 선언하고 바뀌지 않는 값.



:point_up:단, ```var```를 제외한 ```let```과 ```const```는 한번 사용했으면 똑같은 이름으로 재선언 하지 못함  

```js
let value = 1;
let value = 2;

// 중복선언으로 인한 오류 발생
// SyntaxError: /src/index.js: Identifier 'value' has already been declared.
```

## 02. 데이터타입 (null, undefined, NaN)
- ```null```  
값이 없다고 고의적으로 설정한 빈 값.

- ```undefined```  
우리가 설정하지 않아 없는 값.

- ```NaN```  
Not A Number.

:point_up: 단, 숫자에서 ```null```은 ```0```으로, ```NaN```은 ```undefined```로 나온다.

