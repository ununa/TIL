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

### findIndex / find / filter
배열 안에 있는 값이 숫자, 문자열, 또는 불리언이라면 찾고자 하는 항목이 몇번째 원소인지 알기위해 indexOf를 사용하면 된다.  
하지만 배열 안에 있는 값이 객체이거나 배열이라면 indexOf로 찾을 수 없다.

``` js
const todos = [
  {
    id: 1,
    text: '입문',
    done: true
  },
  {
    id: 2,
    text: '함수',
    done: true
  },
  {
    id: 3,
    text: '객체와 배열',
    done: true
  },
  {
    id: 4,
    text: '배열 내장함수',
    done: false
  }
];

// [findIndex] id 3인 객체가 몇번째인지 찾으려면 검사하고자 하는 조건을 반환하는 함수를 넣어 찾을 수 있다.
const index = todos.findIndex(todo => todo.id === 3);
console.log(index); // 2

// [find] findIndex와 비슷하지만, 찾아낸 값 자체를 반환
const index_find = todos.find(todo => todo.id === 3);
console.log(index_find); // {id: 3, text: "객체와 배열", done: true}

// [filter] 배열에서 특정 조건을 만족하는 값들만 따로 추출하여 새로운 배열로 만듬. 
// done 값이 false인 항목들만 따로 추출해서 새로운 배열로 만들기.
const tasksNotDoen = todos.filter(todo => todo.done === false);
// const tasksNotDoen = todos.filter(todo => !todo.done);
console.log(tasksNotDoen); // [{id: 4, text: "배열 내장함수", done: false}];
```


### splice / slice / shift / pop / unshift

``` js
const numbers = [10, 20, 30, 40];

// [splice] 배열에서 특정 항목을 제거할 때 사용
const index = numbers.indexOf(30);
numbers.splice(index, 1);
console.log(numbers); // [10, 20, 40]

// [slice] 배열을 잘라낼 때 사용 (기존 배열에 대한 간섭없음. 새 배열)
// 또한 2개의 파라미터를 넣게 되는데 첫번째 파라미터는 어디서부터 자를지, 두번째 파라미터는 어디까지 자를지를 의미.
const sliced = numbers.clice(0, 2); // 0부터 시작해서 2전까지
console.log(sliced); // [10, 20]
console.log(numbers); // [10, 20, 30, 40]

// [shift]는 첫번째 원소를 배열에서 추출함. (배열에 속한 해당 원소는 사라짐)
const value = numbers.shift();
console.log(value); // 10
console.log(numbers); // [20, 30, 40]

// [pop]은 마지막 항목을 추출함. (배열에 속한 해당 원소는 사라짐)
const value_pop = numbers.pop();
console.log(value_pop); // 40
console.log(numbers); // [10, 20, 30]

// [unshift]는 shift의 반대로, 배열의 맨 앞에 새 원소를 추가함.
numbers.unshift(5);
console.log(numbers); // [5, 10, 20, 30, 40]



```

### concat
여러개의 배열을 하나의 배열로 합쳐주며, 기존의 배열들에 대한 변화 주지 않음.
``` js
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const concated = arr1.concat(arr2);
console.log(concated); // [1, 2, 3, 4, 5, 6]
```

### join
배열 안의 값들을 문자열 형태로 합쳐줌
``` js
const array = [1, 2, 3, 4, 5];
console.log(array.join()); // 1,2,3,4,5
console.log(array.join(' ')); // 1 2 3 4 5
console.log(array.join(', ')); // 1, 2, 3, 4, 5
```


### reduce★


``` js
// 예제) 주어진 배열에 대하여 총합을 구해야 하는 상황.
const numbers = [1, 2, 3, 4, 5];

// 방법1. forEach
let sum = 0;
numbers.forEach(n => {
  sum += n;
});

// 방법2. reduce
let sum = numbers.reduce((accumulator, current) => accumulator + current, 0);

// reduce console.log 살펴보기
// reduce 함수에는 두 개의 파라미터를 전달하는데, 첫 번째 파라미터는 accumulator, current를 파라미터로 가져와서
// 결과를 반환하는 콜백함수 이며, 두 번째 파라미터는 reduce 함수에서 사용 할 초기값이다.
let sum = numbers.reduce((accumulator, current) => {
  console.log({accumulator, current});
  return accumulator + current;
}, 0)

console.log(sum); // 15

```
<img src="https://i.imgur.com/NhagmTP.png" />

배열을 처음부터 끝까지 반복하면서 우리가 전달한 콜백 함수가 호출되는데, 처음엔 accumulator값이 0이며, 이 값이 0인 이유는 두 번째 파라미터인 초기값을 0으로 설정했기 때문이다.

처음 콜백 함수가 호출되면, 0 + 1을 해서 1이 반환되고, 그 다음 콜백함수가 호출 될 때 반환된 1을 accumulator 값으로 사용한다.

콜백함수가 두 번째로 호출 될 땐 1+2를 해서 3이 되고, 이 값이 세 번째로 호출 될 때의 accumulator가 되며, 이렇게 누적된 값이 최종으로 15로 나타나는 것이다.

``` js
// [reduce]를 이용한 평균 계산하기
// 가장 마지막 숫자를 더하고 나서 배열의 length로 나누어주어야 함.
const numbers = [1, 2, 3, 4, 5];

let sum = numbers.reduce((accumulator, current, index, array) => {
  if(index === array.length - 1) {
    return (accumulator + current) / array.length;
  }
  return accumulator + current;
}, 0);

console.log(sum) // 3
```

### 퀴즈
내장함수를 이용해 숫자 배열이 주어졌을 때 10보다 큰 숫자의 갯수를 반환하는 함수 만들기
``` js

function countBiggerThanTen(numbers) {
  /* 구현해보세요 */
}

const count = countBiggerThanTen([1, 2, 3, 5, 10, 20, 30, 40, 50, 60]);
console.log(count); // 5

```

``` js
function countBiggerThanTen(numbers) {
  /* 구현해보세요 */
  
  // 내가 푼 것.
  return (
    numbers.slice(
      numbers.indexOf(10),numbers.length
    )
  ).length - 1;
  
  // 정답1.
  let count = 0;
  numbers.forEach(n => {
    if (n > 10) {
      count++;
    }
  });
  return count;
  
  // 정답2. 
  return numbers.filter(n => n > 10).length;
  
  // 정답3.
  return numbers.reduce((acc, current) => {
    if (current > 10) {
      return acc + 1;
    } else {
      return acc;
    }
  }, 0);
  
}

const count = countBiggerThanTen([1, 2, 3, 5, 10, 20, 30, 40, 50, 60]);
console.log(count); // 5

export default countBiggerThanTen;

```
