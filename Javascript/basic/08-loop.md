## 08. 반복문
특정 작업을 반복적으로 할 때 사용하는 구문.

### for
가장 기본적인 반복문이며, 특정 값에 변화를 주어가면서 계속 반복한다.  
``` js
for (초기 구문; 조건 구문; 변화 구문;) {
  코드
}
```
``` js
for (let i = 0; i < 10; i++) {
  console.log(i); // 0 1 2 3 4 5 6 7 8 9
}
```

### 배열과 for
``` js
const names = ['댕댕', '메옹', '풍뎅이'];

for(let i = 0; i < names.length; i++) {
  console.log(names[i]); // 댕댕 메옹 풍뎅이
}
```

### while
특정 조건이 참이라면 계속해서 반복하는 반복문.
for문은 특정 숫자를 가지고 숫자의 값을 비교하고, 증감해주면서 반복을 해준다면, while문은 조건을 확인만 하면서 반복을 한다.
때문에 조건문 내부에서 변화를 직접 주어야 함.
``` js
let i = 0;
while (i < 10) {
  console.log(i);
  i++;
}
```

### for...of
배열에 관한 반복문을 돌리기 위해서 만들어진 반복문.
``` js
let numbers = [10, 20, 30, 40, 50];
for (let number of numbers) {
  console.log(number);
}
```

### 객체를 위한 반복문 for...in
객체의 정보를 배열 형태로 받아 올 수 있는 함수
``` js
const cat = {
  name: '야옹이',
  sound: '메옹',
  age: 2
};

console.log(Object.entries(cat));
console.log(Object.keys(cat));
console.log(Object.values(cat));
```
각 함수의 역할  
- ```Object.entries```: ```[[키, 값], [키, 값]]```
- ```Object.keys```: ```[키, 키, 키]```
- ```Object.values```: ```[값, 값, 값]```

객체가 지니고 있는 값에 대한 반복.
``` js
const cat = {
  name: '야옹이',
  sound: '메옹',
  age: 2
};

for (let key in cat) {
  console.log(`${key}: ${cat[key]}`);
}
```

## break와 continue
반복문 안에서 ```break```와 ```continue```를 통해 반복문에서 벗어나거나, 그 다음 루프를 돌게끔 할 수 있다.
``` js
for (let i = 0; i < 10; i++) {
  if (i === 2) continue; // 다음 루프를 실행
  console.log(i); // 0 1 3 4 5
  if (i === 5) break; // 반복문을 끝내기
}
```
i가 2일땐 continue를 하여 원래 console.log를 해야 하지만 그 코드를 수행하지 않고 바로 3으로 넘어감.  
i가 5일땐 break를 하여 반복문을 종료 시킴.
