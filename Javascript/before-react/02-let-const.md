
## 02. let과 const로 변수 선언하기
```let```, ```const``` 는 변수 선언시 지역변수가된다. 따라서 함수 스코프 안에서 ```left```으로 선언한 변수는 함수 밖에서 호출 할 수 없다.
- ```const```는 선언한 변수는 선언 이후에 값을 바꿀 수 없고
- ```let```으로 선언한 변수는 바꿀 수 있음

``` js
const name = "David";
let age = 28;
var occupation = "Software Engineer";
```

### 둘 중 무얼 써야 하나?
정해진 규칙이 있는 것은 아니며, 변수 선언은 ```const```로 하는게 좋다고 한다. 프로그램을 만들다 보면 ```const```로 선언한 변수를 변경해야 할 경우가 생길텐데 그 때가 ```const```를 ```let```으로 바꿔야 할 시점이다.

### React에서 어떻게 쓰이나?
변수가 필요한 모든 곳에 쓰임.
``` javascript

import React, { Component } from 'react';

class App extends Component {
  // class content
  render(){
    const greeting = 'Welcome to React';
    return (
      <h1>{greeting}</h1>
    )
  }
}
```
greeting 변수는 어플리케이션의 전체 생명주기(lifecycle)동안 변하지 않기 때문에, ```const``` 키워드를 사용해 변수를 선언한다.
