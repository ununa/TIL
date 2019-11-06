## 09. 배열 내장함수

### forEach

``` js
const superheroes = ['아이언맨', '캡틴 아메리카', '토르', '닥터 스트레인지'];

/*
for (let i = 0; i < superheroes.length; i++) {
  console.log(superheroes[i]);
}
*/
superheroes.forEach(hero => {
  console.log(hero);
});
```
각 원소에 대하여 처리하고 싶은 코드를 함수로 넣어줌. 이 함수의 파라미터 hero는 각 원소를 가르키게 됨.  
이렇게 함수형태의 파라미터를 전달하는 것을 콜백함수라고 부르며, 함수를 등록하면 forEach가 실행을 해줌.


### map
map은 배열 안의 각 원소를 변환할 때 사용 되며, 이 과정에서 새로운 배열이 만들어진다.
``` js
const array = [1, 2, 3, 4, 5, 6, 7, 8];
const squared = [];

// forEach문
array.forEach(n => {
  squared.puch(n * n);
})

/* for 문
for (let i = 0; i < array.length; i++) {
  squared.push(array[i] * array[i]);
}
*/

console.log(squared); // [1, 4, 9, 16, 25, 36, 49, 64];
```
map을 사용하면
``` js
const array = [1, 2, 3, 4, 5, 6, 7, 8];

const square = n => n * n;
const squared = array.map(square);
console.log(squared);
```
map 함수의 파라미터로는 변화를 주는 함수를 전달. 이를 변화함수라 부름.   
변화함수 square는 파라미터 n을 받아와서 이를 제곱으로 해줌.   
array.map 함수를 사용 할 때 square를 변화함수로 사용함으로서, 내부의 모든 값에 대하여 제곱을 하여 새로운 배열을 생성함.  
변화 함수를 꼭 이름 붙여서 선언 할 필요는 없음.
``` js
const suared = array.map(n => n * n);
console.log(squared);
```

### indexOf
원하는 몇번째 원소인지 찾아주는 함소
``` js
const superheroes = ['아이언맨', '캡틴 아메리카', '토르', '닥터 스트레인지'];
const index = superheroes.indexOf('토르');
console.log(index); // 2
```

### findIndex
배열 안에 있는 값이 숫자, 문자열, 또는 불리언이라면 찾고자 하는 항목이 몇번째 원소인지 알기위해 indexOf를 사용하면 된다.  
하지만 배열 안에 있는 값이 객체이거나 배열이라면 indexOf로 찾을 수 없다.
