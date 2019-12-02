# 모듈 패턴(Module Pattern)
- javascript의 코드 관리 기법 중 하나로 객체 핸들링을 위한 방법론 중 하나
- 객체에 유효범위를 주어 private, public을 구분하여 캡슐화 할 때 사용 하는 방법
- ```Namespace pattern```에 ```Lexical Scope```를 추가한 것으로 보면 됨
> Module Pattern이란, 즉시 실행 함수(Immediately Invoked Function)에  
> ```this```인자를 넘겨주고 함수 내부에서 ```exports```란 인자로 접근할 수 있는 패턴
``` js
// 패턴 적용 전: global scope에 변수, 함수 모두 존재하는 상황
var coutGlobal = 0;
var increaseCountGlobal = function(){
  return (++count);
}
var decreaseCountGlobal = function(){
  return (--count);
}

// 패턴 적용 후: testModule 이라는 객체에 모두 집어 넣음
var test = (function(){
  var count = 0;
  return {
    increaseCount: function(){
      return (++count);
    },
    decreaseCount: function(){
      return (--count);
    }
  }
})();
```
> 모듈 패턴을 사용하게 되면 두 함수 ```increaseCount```, ```decreaseCount```에서 ```this```인자의 사용없이  
> 클로저 원리를 통해 ```count```변수에 접근할 수 있다.  
> ```count```변수는 ```Java```에서의 접근 제어자인 ```private```과 같이 처리 되었다.  
> 즉, 외부에서는 접근이 불가능한 변수이며, 이렇게 모듈 패턴을 사용하면 보다 객체지향적인 코드를 작성할 수 있다.
``` js
// 네임스페이스 패턴과 함께 사용하기
// app이라는 전역 객체에 testModule이라는 모듈을 추가시킴.
var app = app || {};
app.testModule = (function(){
  var count = 0;
  return {
    increaseCount: function(){
      return (++count);
    },
    decreaseCount: function(){
      return (--count);
    }
  }
})();
```
