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
