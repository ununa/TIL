# ES2015 모듈(Modules)
자바스크립트에서 모듈을 이용하면 전역 네임 스페이스 오염없이 값을 내보내고 가져올 수 있다.
* 네임 스페이스(NameSpace): 구분이 가능하도록 정해놓은 범위나 영역을 의미. 이름 공간을 선언하여 다른 공간과 구분.
> ES6의 모듈은 Javascript 코드를 담고 있는 파일을 말한다. global scrope에서의 변수명 충돌을 방지하기 위해
> 모듈화 방식을 사용하는데, 모듈안에서 자동적으로 strict 모드로 처리 된다.

## CommonJS 모듈
- JS에서는 CommonJs 모듈 문법을 주로 사용했는데,
- 이 방식은 모듈을 불러오기 위해 ```require```를 사용하고,
- 모듈을 내보내기 위해 ```module.exports```문법을 사용한다.
``` js
// module 내보내기
module.exports = sum = (a, b) => {
  return a + b;
}

// module 가져오기
const sum = requre("./sum");
console.log(sum(1, 2));
```

## import, export
- ES6에서는 새롭게 ```import```와 ```export``` 구문이 추가됨
- ```export``` 문을 사용해 내보낼 함수나 객체를 내보낼 수 있음
- ```import``` 문을 사용해 모듈을 불러옴.

### Creating Modules
``` js
// lib/math.js
export function sum(x, y) { return x + y }
export var pi = 3.141593

// app.js
import * as math form "lib/math"
math.sum(math.pi, 2)

// app2.js
import {sum, pi} from "lib/math"
sum(pi, 2)
```
- 이때 하나의 파일에서 단일 값이나 단일 객체, 단일 함수, 단일 클래스를 내보내는 경우라면
- ```export default```와 같이 default 구문을 추가해 내보내기할 경우 단일 값으로 import 할 수 있음.
- ```default```키워드는 export하는 type을 의미하며, default로 지정했을 떄 가장 simple한 방법이다.
``` js
// src/utils/utility.js
let calc = {
  add(x, y) {
    return x + y;
  },
  multiply(x, y) {
    return x * y;
  }
}

export default calc;

// src/main.js
// export 할 때 default로 export 했기 때문에 주소값만 잘 맞으면 calc란 이름은 달라도 상관없다.
import calc from './utils/utility';

calc.add(4, 5);
calc.multiply(4, 5);
```
- ```import```할 자바스크립트 파일은 같은 폴더에 위치하고 있어야 한다.
- webpack이 제공하는 기능 중 하나인 bundle과 혼동하여서는 안된다.
- script태그를 통해서 html 코드에 추가해줘야 한다.


### Named Exports
특정 ```function```을 ```export```한 경우에, ```function```의 이름을 통해서 ```import```할 수 있다.
``` js
// flash-message.js
export function alertMessage(message) {
  alert(message);
}
export function logMessage(message) {
  console.log(message);
}

// app.js
import { alertMessage, logMessage } from './flash-message';
alertMessage('Hello'); // alert execute!
logMessage('world'); // world
```

