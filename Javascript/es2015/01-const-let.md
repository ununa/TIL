# ES2015 const & let

- ```const```와 ```let```은 ES6에 새롭게 추가된 변수 선언자. 
- 블록 수준의 유효범위를 갖음.
- 변수는 중괄호(```{}```) 내부에서만 유효

## let
``` js
// var
console.log(x);  //-> undefined. 호이스팅 발생.
var x = 10; 

// let
console.log(y); //-> ReferenceError: y is not defined.
let y = 10; 
```

### 블록 스코프
```let```은 블록 스코프를 갖는 변수를 선언할 때 사용.
``` js
  // var
  for(var i = 0; i < 5; i++) {
    setTimeout(function(){ //-> 클로저
      console.log(i); //-> 5 5 5 5 5
    }, (i)*1000);
  }
  
  // let
  for(let i = 0; i < 5; i++) {
    setTimeout(function(){
      console.log(i); //-> 0 1 2 3 4
    }, (i)*1000);
  }
```
블록 유효범위를 가지는 ```let```을 사용할 경우 반복문이 실행될 때마다 새롭게 블록 내부에서 변수 ```i```를 선언해서 사용하게 된다.

## const
- 블록 유효범위를 갖는 상수를 선언할 때 사용.
- ```let``` 혹은 ```var```와 달리 반드시 선언시 값을 초기화 해야한다.
``` js
  const alice = "Alice";
  
  alice = "Dinah" //-> TypeError: Assignment to constant variable.
```
