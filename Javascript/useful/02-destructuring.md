# 비구조화 할당 (구조분해) 문법

### 비구조화 할당
``` js
// 객체 안에 있는 값을 추출한 뒤 변수 혹은 상수로 바로 선언
const object = { a: 1, b: 2 };
const { a, b } = object;

console.log(a); // 1
console.log(b); // 2
```

### 함수의 파라미터에서도 비구조화 할당
``` js
const object = { a: 1, b: 2 };

function print({ a, b }) {
  console.log(a);
  console.log(b);
}

print(object);


// 만약 b 값이 주어지지 않았을 때
const object = { a: 1 };

function print({ a, b }) {
  console.log(a);
  console.log(b);
}

print(object); // a -> 1, b -> undefined
```

### 비구조화 할당시 기본값 설정
``` js
const object = { a: 1 };

function print({ a, b = 2 }) {
  console.log(a);
  console.log(b);
}

print(object); // a -> 1, b -> 2
```

### 비구조화 할당시 이름 바꾸기
```:``` 문자를 사용해서 이름을 바꿔줄 수 있다.
``` js
const animal = {
  name: '멍멍이',
  type: '개'
};

// const nickname = animal.name; 
const { name: nickname } = animal // animal 객체 안에 있는 name을 nickname 이라고 선언하겠다.

console.log(nickname);
```

### 배열 비구조화 할당
> 비구조화 할당은 객체에서만 할 수 있는 것이 아니며, 배열에서도 할 수 있다.  
> 배열 안에 있는 원소를 다른 이름으로 새로 선언해주고 싶을 때 사용하면 매우 유용함  
> 객체 비구조화 할당과 마찬가지로, 기본값 지정이 가능.

``` js
const array = [1, 2];
const [one, two] = array;

console.log(one);
console.log(two);

// 배열 비구조화 할당
const array = [1];
const [one, two = 2] = array;

console.log(one);
console.log(two);
```

### 깊은 값 비구조화 할당
객체의 깊숙한 곳에 들어있는 값을 꺼내는 방법
``` js
const deepObject = {
  state: {
    information: {
      name: 'ununa',
      languages: ['korean', 'english', 'chinese']
    }
  },
  value: 5
};
```

#### name, languages, value 값들을 밖으로 꺼내기
``` js
// 방법1. 비구조화 할당 문법을 두번 사용 
const { name, languages } = deepObject.state.information;
const { value } = deepObject;

/*
const extracted = {
  name: name,
  languages: languages,
  value: value
};
*/
const extracted = {
  name,
  languages,
  value
};

console.log(extracted); // {name: 'ununa', languages: Array[3], value: 5}
```

#### 한 번에 모두 추출하는 방법(object-shorthand)
``` js
const {
  state: {
    information: { name, languages }
  },
  value
} = deepObject;

const extracted = {
  name,
  languages,
  value
};

console.log(extracted);
```

