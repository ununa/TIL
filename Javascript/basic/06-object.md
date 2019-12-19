## 06. 객체
서로 연관된 함수와 변수를 담아 놓는 상자.  
즉,  ```사전``` 이라고 비유할 있으며 단어를 ```키(key)```, 설명을 ```값(value)```  
이렇게 키와 값의 쌍으로 이루어진 데이터의 ```객체```라 부른다.


```코드``` < ```함수``` < ```객체```

``` js
const cat = {
  name: '메옹',
  age: 2
  // key(문자열) : value
  // key === property === 속성
  // 객체 속성의 출력 순서는 임의적이다(arbitrary order)
  // 브라우저 마음대로 나오니, 객체 순서의 의존해서 프로그래밍 하지 말 것.
};
let key = 'name';
```
> ```cat```이라는 객체를 정의  
> 선언 할 때에는 중괄호(```{ }```)를 이용해서 한다.  
> 객체 내부에 키와 값은 콜론(```:```)으로 구분해 작성하며, 각각의 항목들은 콤마로 구분한다.  
> key는 어떠한 값을 불러오기 위한 방법이니 객체 내에서 유일해야 한다.
> 또한 키에 해당하는 부분은 공백이 없어야 하며, 공백이 있을시엔 따옴표로 감싸서 문자열로 넣어줘야한다.  
> ```'key with space': true```  // 띄어쓰기는 가능하지만 되도록이면 쓰지 않기 __ 이용하기 

## 객체 사용하기
#### 1. new와 Object 생성자 이용
```new Object()```
``` js
const obj = new Object;
```

#### 2. 객체 리터럴 이용
```{ }```
``` js
const obj = {};
```

#### 3. new와 사용자 정의 생성자 이용
```new Person()```


## 객체 내부의 프로퍼티 값을 불러오기.
**방법1.**
``` js
// 1. 객체의 이름뒤에 점(.)을 찍고 키를 명시
console.log(cat.name); // 메옹

// 2. 대괄호를 이용해서 원하는 값 조회
console.log(cat['name']); // 메옹

// 3. [key]
console.log(cat[key]); // 메옹
```
**방법2.**
``` js
for(var i in cat){
    console.log(i);
    console.log(cat[i]);
    // name
    // 메옹
    // age
    // 2
}
```

## 객체에 새로운 프로퍼티와 값 추가하기.
``` js
cat.sound = "메에에옹";
console.log(cat) // => { name: '메옹', age: 2, sound: '메에에옹' }
```
! 만약, 해당 프로퍼티가 이미 존재한다면 값을 덮어씌움.

## 프로퍼티 삭제
cat 객체에서 sound 키-값 쌍은 삭제 됨.
``` js
delete cat.sound;
```

#### 잠깐! 용어정리.
객체에 속해있는 함수는 ```메소드```   
객체에 속해있는 변수는 ```프로퍼티```
```
List.setLayout(){
   ...
};

// 객체.메소드(){
//   리터럴
// };
```

```
const ironMan = {
  name: '토니 스타크'
};

// const 객체 = {
//   프로퍼티: 값
// };
```


## 함수에서 객체를 파라미터로 받기
함수를 만들고, 객체를 파라미터로 받아와서 사용해보기
``` js
const abyssinian = {
  name: '아비시니안',
};

function print(cat) {
  const text = `${cat.name}은 정말 귀여워!`;
  console.log(text);
}

print(abyssinian);  // 아비시니안은 정말 귀여워!
```


## 객체 비구조화 할당
객체 구조 분해하기
``` js
const abyssinian = {
  name: '아비시니안',
};

function print(cat) {
  const { name } = cat; // 값들을 추출한 뒤 새로운 상수로 선언.
  const text = `${name}은 정말 귀여워!`;
  console.log(text);
}

print(abyssinian);  // 아비시니안은 정말 귀여워!
```

파라미터 단계에서 객체 비구조화 할당 하기.
``` js
const abyssinian = {
  name: '아비시니안',
};

function print({ name }) {
  const text = `${name}은 정말 귀여워!`;
  console.log(text);
}

print(abyssinian);  // 아비시니안은 정말 귀여워!
```


## 객체 안에 함수 넣기
``` js
const cat = {
  name: '나비',
  sound: '메오옹~~',
  say: function say() {
    console.log(this.sound);
  }
};

cat.say(); // 메오옹~~
```
함수가 객체안에 들어가게 되면, ```this```는 자신이 속해있는 객체를 가르키게 된다.

함수를 선언 할 때에는 이름이 없어도 됨.
``` js
const cat = {
  name: '나비',
  sound: '메오옹~~',
  say: function() {
    console.log(this.sound);
  }
};

cat.say(); // 메오옹~~
```

단, 화살표 함수로 선언한다면 제대로 작동하지 않는데,
이유는 function으로 선언한 함수는 this가 자신을 속한 객체를 제대로 가르키게 되는데,
화살표 함수는 그렇지 않다.

### Getter 함수와 Setter 함수
객체를 만들고 나면, 객체안의 값을 수정 할 수 있게 도와주는 함수.
#### Getter
``` js
const numbers = {
  a: 1,
  b: 2,
  get sum() {
    console.log('sum 함수가 실행됩니다!');
    return this.a + this.b;
  }
};

console.log(numbers.sum);
numbers.b = 5;
console.log(numbers.sum);
```
```numbers.sum()```을 한 것이 아니라 ```numbers.sum```을 조회했을뿐인데,
함수가 실행되고 그 결과값이 출력됨.
```Getter함수```는 특정 값을 조회 할 때 우리가 설정한 함수로 연산된 값을 반환함.
#### Setter
``` js
const numbers = {
  _a: 1,
  _b: 2,
  sum: 3,
  calculate() {
    console.log('calculate');
    this.sum = this._a + this._b;
  },
  get a() {
    return this._a;
  },
  get b() {
    return this._b;
  },
  set a(value) {
    console.log('a가 바뀝니다.');
    this._a = value;
    this.calculate();
  },
  set b(value) {
    console.log('b가 바뀝니다.');
    this._b = value;
    this.calculate();
  }
};

console.log(numbers.sum); // 
numbers.a = 5; // a가 바뀝니다. calculate
numbers.b = 7; // b가 바뀝니다. calculate
numbers.a = 9; // a가 바뀝니다. calculate
console.log(numbers.sum); // 16
console.log(numbers.sum); // 16
console.log(numbers.sum); // 16
```
a 혹은 b 값이 바뀔 때마다 sum 값을 연산함.  
```numbers.a = 5``` 에서 5 를 함수의 파라미터로 받아옴.  
객체안에 _a, _b 라는 숫자를 선언해주고, 이 값들을 위한 getter 와 Setter 함수를 설정.

아직 Getter, Setter에 대한 개념이 부족해 더 알아봐야겠음
