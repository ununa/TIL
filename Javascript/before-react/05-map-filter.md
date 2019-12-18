# 05. map과 filter
맵과 필터는 ES5의 배열이며, 특히 데이터를 가공할 때 유용하게 쓰인다.

### API를 통해 받아온 데이터(JSON 배열)
``` js
const users = [
  { name: 'Nathan', age: 25 },
  { name: 'Jack', age: 30 },
  { name: 'Joe', age: 28 },
];
```

### 배열의 각 요소를 map을 이용해 뽑아내 render()에서 사용하기
``` js
import React, { Component } from 'react';

class App extends Component {
  // class content
  render(){
    const users = [
      { name: 'Nathan', age: 25 },
      { name: 'Jack', age: 30 },
      { name: 'Joe', age: 28 },
    ];

    return (
      <ul>
        {users
          .map(user => <li>{user.name}</li>)
        }
      </ul>
    )
  }
}
```

### data를 필터링(filter)해서 render()에서 사용하기
``` js
<ul>
  {users
    .filter(user => user.age > 26)
    .map(user => <li>{user.name}</li>)
  }
</ul>
```
