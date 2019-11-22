## 01. 삼항 연산자

``` JS
// 사용법.
조건 ? true 일때 : false 일때;

// 라인의 길이가 길어진다면,
조건
? true 일때 
: false 일때;

```
``` JS
const array = [];
let text = array.length === 0 ? '배열이 비어있습니다.' : '배열이 비어있지 않습니다.';

console.log(text); // 

```

## 02. Truthy and Falsy(문법X, 개념O)
Truthy: true / Falsy: false

``` js
// true
console.log(!undefined);
console.log(!null);
console.log(!0);
console.log(!'');
console.log(!NaN);

// false
console.log(!3);
console.log(!'hello');
console.log(!['array?']);
console.log(![]);
console.log(!{ value: 1 });
```

``` js
// 삼항연산자와 합치기
const value = { a: 1 };
const truthy = value ? true : false;
// const truthy = !!value;
```

## 03. 단축 평가(short-circuit evaluation) 논리 계산법
### && 연산자로 코드 단축시키기
A가 Truthy 한 값이라면, B가 결과값이 됨.
반면, A가 Falsy 한 값이라면 결과는 A가 됨.
특정 값이 유효할때에만 어떤 값을 조회하는 작업을 해야 할 때 매우 유용함.
``` js
const dog = {
  name: '멍멍이'
};

function getName(animal) {
  /*
  if (animal) {
    return animal.name;
  }
  return undefined;
  */
  
  return animal && animal.name;
}

const name = getName();
console.log(name);
```

### || 연산자로 코드 단축시키기
|| 연산자는 어떤 값이 Falsy 하다면 대체로 사용 할 값을 지정해줄 때 매우 유용하게 사용 할 수 있다.
``` js
const namelessDog = {
  name: ''
};

function getName(animal) {
  const name = animal && animal.name;
  /*
  if (!name) {
    return '이름이 없는 동물입니다';
  }
  return name;
  */
  return name || '이름이 없는 동물입니다';
}

const name = getName(namelessDog);
console.log(name); // 이름이 없는 동물입니다.
```


### 04. 함수의 기본 파라미터
원의 넓이는 구하는 함수

``` js
function circle(r) {
  return Math.PI * r * r; // Math.PI는 원주율 파이(π) 값을 가리킴.
}
const area = circle(4);
console.log(area);
```
```r``` 값이 없다면 ```NaN```이 나오게 되는데, 기본 값을 1로 사용되도록 설정해보기.
``` js
// ES5
function circle(r) {
  const radius = r || 1;
  return Math.PI * r * r;
}

// ES6
function circle(r = 1) {
  return Math.PI * r * r;
}

// ES6 & 화살표 함수
const circle = (r = 1) => Math.PI * r * r;


const area = circle();
console.log(area);
```

### 05. 조건문 더 스마트하게 쓰기
#### 특정 값이 여러 값중 하나인지 확인해야 할 때
```js
function isAnimal(text) {
  return(
    text === '고양이' || text === '개' || text === '거북이'
  );
}

// 방법1. 배열을 만들고 배열의 includes 함수 사용하기.
function isAnimal(name) {
  const animals = ['고양이', '개', '거북이'];
  return animals.includes(name);
}

// 방법2. 배열 + 화살표 함수
const isAnimal = name => ['고양이', '개', '거북이'].includes(name);

console.log(isAnimal('개')); // true
console.log(isAnimal('노트북')); // false
```

#### 값에 따라 다른 결과물을 반환 해야 할 때
ex) 동물 이름을 받아오면, 동물의 소리를 반환.
``` js
function getSound(animal) {
  if (animal === '개') return '멍멍';
  if (animal === '고양이') return '메에옹';
  return '...';
  
  // 방법1. switch case문
  switch(animal) {
    case '개':
      return '멍멍';
    case '고양이':
      return '메에옹';
    default:
      return '...';
  }
  
  // 방법2. 객체
  const sounds = {
    개: '멍멍',
    고양이: '메에옹'
  };
  return sounds[animal] || '...';
  
  // 방법3. 객체 + 값에 따라 실행하는 코드 구문이 다를 때.
  const tasks = {
    개() {
      console.log('멍멍');
    },
    고양이() {
      console.log('메에옹');
    }
  };
  if(!tasks[animal]){
    console.log('...')
  }
  tasks[animal]();
}

console.log(getSound('개')) // 멍멍
```
