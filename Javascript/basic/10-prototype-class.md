## 10. 프로토타입과 클래스

### 객체(다시한번!!)
``` js
var kitty = {
  name: "Dinah",
  age: 3,
  species: "Short hair",
  health: 5,

  eat: function() {
    this.health = this.health + 1;
  },
  run: function() {
    console.log(this.name + " Running!!");
  }
}

console.log(kitty.name);  //-> Dinah
console.log(kitty.health);  //-> 5

kitty.eat();
console.log(kitty.health);  //-> 6

kitty.run();  //-> Dinah Running!!
```

### 프로퍼티(Property)
자바스크립트의 객체에서 프로퍼티는 이름이 붙어있는 값을 나타낸다.

### 메서드(Method)
함수가 프로퍼티에 저장될 경우 이러한 함수를 메서드라고 부르며,  
**메서드는 객체 내에 정의된 함수**로, 객체의 프로퍼티 명이 함수의 이름으로 쓰인다.   
호출시엔 ```객체명.메서드명()```을 사용.

### this
this는 함수가 실행될때 그 함수를 호출한 객체를 가리키는 키워드인데 함수에서 참조하는 메모리 영역을 나타낸다.   
객체 메서드 내부의 ```this```는 객체를 가리키며, 위 코드에서는 ```kitty```라는 객체를 가리키게 된다.

자바스크립트에서 ```this```는 함수가 호출되어 실행되는 시점에 결정되며, ```this```의 값은 함수가 호출 되었을 때  
그 함수가 속해있던 객체를 가리키게 되며, 호출될 때 ```this```가 가리키는 객체가 변경될 경우 ```this```의 값도 바뀌게 된다.

**this가 가리키는 대상**
- 전역: 전역에서 this의 값은 전역객체를 가리킴. Node.js의 경우 ```global```객체를, 웹브라우저의 경우 ```window``` 객체를 가리킴
- 전역 함수: 전역에서 함수를 호출하게 되면 함수 내부의 this는 전역 객체를 가리킴, 이는 함수를 전역에서 선언하고 호출할 경우 함수는 전역객체 내부에 정의되기 때문.
- 객체: 생성자로 생성한 객체 내부에서의 ```this```는 생성한 객체를 가리킴. 인스턴스 메서드 내부에서도 역시 메서드를 호출한 객체를 가리키게 됨.
- 이벤트 핸들러: 이벤트 핸들러 내부에서는 이벤트가 발생한 요소 객체를 가리킴.

### 객체 생성자
``` js
const dinah = new Kitty("Dinah", 5, "Short hair");
```
함수를 통해서 새로운 객체를 만들고 그 안에 넣고 싶은 값 혹은 함수들을 구현 할 수 있게 해준다.
- 보통 함수의 이름을 **대문자**로 시작(PascalCase 표기법)하고, 새로운 객체를 만들 때에는 ```new```키워드를 앞에 붙여주어야 함.

### 생성자 함수.
``` js
function Kitty(name, age, species) {
  this.name = name;
  this.age = age;
  this.species = species;
  this.health = 5;
  
  this.eat = function() {
    this.health = this.health + 1;
  };
  
  this.run = function() {
    console.log(this.name + " Running!!");
  };
}
```
객체를 생성하는 함수.
생성자 함수의 이름은 다른 함수와 구분하기 위해 PascalCase 표기법(첫글자가 대문자로 시작)을 사용.  
기존 함수와 동일한 방법으로 선언하고 new 연산자를 붙여서 호출하면 해당 함수는 생성자 함수로 동작.
```new```연산자를 통해 생성한 객체를 **인스턴스**라고 부름.
``` js
var dinah = new Kitty("Dinah", 5, "Short hair");
var cheshire = new Kitty("Cheshire", 10, "Scottish");

console.log(dinah.age);    // 5
console.log(dinah.run());  // Dinah Running!!
console.log(cheshire.name);  // Cheshire
```
위 예에서 ```new```키워드를 이용해 객체를 생성할 때 넘겨준 인수는 ```this```를 사용해 객체의 프로퍼티에 대입됨.  
따라서 생성한 객체의 프로퍼티는 객체 생성 시 넘겨준 인수를 이용해 초기화 됨.
생성자를 이용해 객체를 생성하면 동일한 타입의 객체를 여러개 생성 할 수 있으므로 효율적으로 객체를 관리할 수 있음.
- 생성자 함수 이름은 PascalCase 표기법(첫글자가 대문자로 시작)을 사용. 이것은 생성자 함수임을 인식하도록 도움을 준다.
- ```this```는 생성자 함수가 생성할 인스턴스(instance)를 가리킨다.
- ```this```에 연결(바인딩)되어 있는 프로퍼티와 메소드는 ```public```(외부에서 참조 가능)하다.
- 생성자 함수 내에서 선언된 일반 변수는 ```private```(외부에서 참조 불가능)하다.

### Prototype
자바스크립트의 모든 객체는 프로토타입(prototype)이라는 객체를 가지고 있으며,  
모든 객체는 그들의 프로토타입으로부터 프로퍼티와 메소드를 상속 받는다.
이처럼 자바스크립트의 모든 객체는 최소한 하나 이상의 다른 객체로부터 상속을 받으며, 이때 상속되는 정보를 제공하는 객체를 프로토타입(prototype)이라고 한다.
프로토타입은 객체 생성자 함수 아래에 ```.prototype.[원하는키] = ``` 코드를 입력하여 설정 할 수 있음.

``` js
function Kitty(name, age, species) {
  this.name = name;
  this.age = age;
  this.species = species;
  this.health = 5;
}

Kitty.prototype.eat = function() {
  this.health = this.health + 1;
};

Kitty.prototype.run = function() {
  console.log(this.name + " Running!!");
};

var dinah = new Kitty("Dinah", 5, "Short hair");
var cheshire = new Kitty("Cheshire", 10, "Scottish");

console.log(dinah.age);    // 5
console.log(dinah.run());  // Dinah Running!!
console.log(cheshire.name);  // Cheshire
```

### 프로토타입 체인(prototype chain)
객체 이니셜라이저를 사용하여 생성된 같은 타입의 객체들은 모두 같은 프로토타입을 가지게 된다.
또한 ```new``` 연산자를 사용해 생성한 객체는 생성자의 프로토타입을 자신의 프로토타입으로 상속 받는다.
