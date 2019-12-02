# ES2015 문자열 조작하기
## 템플릿 리터럴
- 문자열을 표기하기 위해 기존에 사용되던 작은 따옴표 및 큰 따옴표(```'', ""```) 외에 백틱 기호(``)를 이용할 수 있음
- 백틱 기호로 둘러싼 문자열은 템플릿 리터럴 표기법을 사용할 수 있게 됨.
- 개행을 위해 개행할 문장의 끝에 일일이 (```\n```)을 사용해야 했지만 템플릿 리터럴을 사용하면 문자열 개행을 손쉽게 처리할 수 있음.
- 단, 아직까진 IE에서 지원 안함.

``` js
const str = `Oh dear! Oh dear!
I shall be too late!`

console.log(str);
/* 결과
Oh dear! Oh dear!
I shall be too late!
*/

let stream = `
<div class="row">
  <div class="col-xs-2 logo"><img src="logo.png"></div>
  <div class="col-xs-7 desc"><p>Online</p></div>
</div>
`;
```

## 문자열 보간(String Interpolation)
- 템플릿 리터럴 사용 시 ```${}``` 템플릿을 이용해 문자열 사이에 손쉽게 값을 대입할 수 있음
- 이를 문자열 보간이라고 표현함
- 플레이스 홀더 기호 내부에는 자바스크립트 표현식이 올 수 있으며, 문자열 내부에 손쉽게 변수 값이나 표현식 값을 삽입할 수 있음


``` js
var alice = { name: 'Alice', place: 'Wonderland' };
var place = alice.place || "Nowhere";
var message = `${alice.name} in ${place}`

console.log(message);  //-> Alice in Wonderland


// 예시
let stream = `
<div class="row ${online ? "online" : ""}">
  <div class="col-xs-2 logo"><img src=${logo}></div>
  <div class="col-xs-3 title"><a href=${url} target="_blank">${name}</a></div>
  <div class="col-xs-7 desc"><p>${online ? status : "Offline"}</p></div>
</div>
`;
```

## string 객체
특정 문자열 존재여부 확인하기.
``` js
var str = "As I was going to Saint Ives";

// str이 인수의 값으로 시작하는지 확인
str.startsWith("As")        // true
str.startsWith("going", 9)  // true, index 9에서 시작

// str이 인수의 값으로 끝나는지 확인
str.endsWith("Ives")        // true
str.endsWith("going", 14)   // true, index 14를 끝으로 간주

// str이 인수의 값을 포함하는지 확인
str.includes("going")       // true
```
