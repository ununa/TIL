# 네임 스페이스 패턴(NameSpace Pattern)
전역 변수를 기초로 하는 JavaScript의 단점 때문에,
여러 스크립트가 한 페이지 안에 함꼐 있는 소스코드에서는 변수가 많아질 수록 이름이 겹칠 우려가 있다. 
네임스페이스를 오염시키지 않기 위한 여러가지 패턴들을 살펴보자.

## 객체 리터럴 네임 스페이싱(Object Literal NameSpacing)
- 하나의 전역 객체를 생성한 다음, 모든 함수, 객체, 변수를 이 전역객체에 추가하여 구현하는 방법
- 이 방법은 JS 라이브러리나 *서드 파티 코드¹*와의 이름 충돌을 방지할 수 있다.
- 하지만 모든 변수, 함수에 상위 객체명을 붙여야 하기 때문에 코드의 양이 많아진다.
- 그러면서 매번 객체에 접근할 때 마다 체인이 길어지고 이름이 중첩된다.
> 서드 파티(Thrid Party): 프로그래밍 개발과 개발자 사이에 ```플러그인, 라이브러리, 프레임워크```를 칭함.
> ```제3자```로써 중간 다리의 역할을 하는 것을 서드파티라고 함.
``` js
// 전역 객체 하나 생성
var globVariable = {};

// 객체의 프로퍼티로 추가
globVariable.num = 1;

// 함수도 추가
globVariable.increaseNum = function(){
  console.log('increase!');
}
globVariable.decreaseNum = function(){
  console.log('decrease!');
}
```

## 범용 네임스페이스 함수
- 이미 있는 것을 재정의하는 일을 방지하기 위하여 사용하는 방법.
- 이를 확인하지 못해 재정의 한다면 내용을 덮어쓰는 문제가 생기기 때문이다.
``` js
// 방법 1.
if(type of app === "undefined"){
  var app = {};
}

// 방법 2. == 방법 1.
var app = app || {};
```
