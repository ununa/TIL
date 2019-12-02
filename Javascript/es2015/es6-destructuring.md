# ES2015 비구조화 할당(Destructuring Assignment)
비구조화 할당 혹은 구조분해 할당을 이용하면 손쉽게 배열, 객체에서 데이터를 추출하여 변수에 할당할 수 있다.

## 객체 비구조화 할당
객체의 값을 각각 할당하기
``` js
// ES5
var myObj = { a: 1, b: 2 };
var a = myObj.a;
var b = myObj.b;

// ES6 객체 비구조화 할당
let { a, b } = = { a: 1, b: 2 };

// ES6 객체에 존재하지 않는 키
let { a, b, c } = = { a: 1, b: 2 }; // -> c: undefined
```
비구조화 할당은 모듈을 ```import```할 때 사용되는 것을 많이 볼 수 있는데,  
```react```에서 컴포넌트 클래스를 불러올 때 비구조화 할당을 사용하는 예시
```js
import React, { Component } from "react";
```

## 배열 비구조화 할당
``` js
// 예시
var list = [1, 2, 3];
var [a, , b] = list;

// 구조분해 할당을 응용하면 각 변수의 값을 손쉽게 바꿀 수 있음
[b, a] = [a, b];

// Spread 연산자 사용(확산 연산자)
const arr = [1, 2, 3, 4, 5];
let [x, y, ...rest] = arr;
// x: 1. y: 2, rest: [3, 4, 5]
```
