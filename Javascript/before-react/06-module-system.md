# 06. ES6 모듈 시스템
ES6 모듈 시스템(module system)은 자바스크립트가 파일(모듈)을 호출(import)하고, 선언하여 내보낼 수 있게(export) 해준다.

### ```src/app.js``` 코드 살펴보기
``` js
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a
            className="App-link"
            href="https://reactjs.org"
            target="_blank"
            rel="noopener noreferrer"
          >
            Learn React
          </a>
        </header>
      </div>
    );
  }
}

export default App;
```

#### 코드 맨 윗줄에 있는 ```import``` 키워드
``` js
import React, { Component } from 'react';
```

#### 코드 맨 아랫줄에 ```export default``` 문
``` js
export default App;
```

### 모듈 문법에 대해 먼저 알기.
모듈은 ```export```키워드를 통해 하나 혹은 다수의 값(객체나 함수, 또는 변수)을 선언하여 외부로 내보낼 수 있게 해주는 자바스크립트 파일.  

#### ```src```폴더에 새로운 파일, ```util.js```만들어보기
``` cmd
touch util.js
```

#### ```util.js```에 함수 작성하기
times 모듈은 default export가 된다.
``` js
export default function times(x) {
  return x * x;
}
```

#### named export 만들기
``` js
export function times(x) {
  return x * x;
}
export function plusTwo(number) {
  return number + 2;
}
```

#### ```src/App.js```에서 export한 함수들을 불러오기
``` js
import { times, plusTwo } from './util.js';
console.log(times(2));
console.log(plusTwo(3));
```

### default export
- 모듈 하나에 여러 개의 ```named exports```가 있을 수 있지만, ```default export```는 딱 하나만 허용됨.
- ```default export```는 ```{}```를 사용하지 않으면서, 상응하는 이름 없이도 ```import```할 수 있음.
``` js
// in util.js
export default function times(x) {
  return x * x;
}
// in app.js
import k from './util.js';
console.log(k(4)); // returns 16
```

### named export
- 반면, ```named export```는 ```{}```을 이용해 import해야하고, 정확한 이름도 명시해 주어야 한다.
- as 키워드를 사용해 별칭을 사용하면, 모듈 이름이 겹치는 경우를 할 수 있다.
``` js
// in util.js
export function times(x) {
  return x * x;
}
export function plusTwo(number) {
  return number + 2;
}
// in app.js
import { times as multiplication, plusTwo as plus2 } from './util.js';
```

#### 절대이름(absolute name)을 이용하며 import 하기
절대 이름을 사용하여 import할 때는 자바스크립트에 이에 상응하는 패키지 이름을 ```node_modules```에서 검색함.  
그러므로 local에 저장된 파일을 import 할 때는, 파일의 위치를 제대로 입력해야함.
``` js
import React from 'react';
```

### React에서 어떻게 쓰이나?
``` js
//index.js file

import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: http://bit.ly/CRA-PWA
serviceWorker.unregister();
```
- ```src/App.js```파일에서 모듈 시스템과 관련된 문법이 쓰인걸 확인할 수 있다.  
- export된 ```App```컴포넌트가 렌더링 되고 있는 ```index.js``` 파일에서도 이를 확인할 수 있다.
- serviceWorker는 다음에 알아보기
- ```./App``` 디렉토리에서 import한 App은 확장자가 없다는 점에서 주목.
- JS파일을 import 할 땐, 확장자를 생략해도 된다.
- 하지만 .css와 같이 다른 종류의 파일은 확장자를 반드시 써 주어야 한다.
- DOM 렌더링에 사용되는 노드 모듈인 ```react-dom```도 import 해주어야 한다.

#### 서비스 워크(service worker)
서비스워커는 React 애플리케이션이 오프라인에서도 작동할 수 있게 해준다. PWA(Progressive Web App)을 학습하면서 서비스 워크를 알아가라.



