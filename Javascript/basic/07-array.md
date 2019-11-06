## 07. 배열
객체는 한 변수 혹은 상수에 여러가지 정보를 담기 위함이었다면, 배열은 여러개의 항목들이 들어있는 리스트와 같다.
#### 숫자 배열
``` js
const array = [1, 2, 3, 4, 5];
```
#### 객체 배열
``` js
const objects = [{ name: '댕댕' }, { name: '메옹' }];
```
#### 배열 조회
```objects[n];```  
첫 번째 항목은 0 부터 시작.
``` js
const objects = [{ name: '댕댕' }, { name: '메옹' }];

console.log(objects);
console.log(objects[0]);
console.log(objects[1]);
```
#### 배열 추가
배열이 지니고 있는 내장 함수 ```push``` 함수를 사용.
``` js
const objects = [{ name: '댕댕' }, { name: '메옹' }];

objects.push({
  name: '장수풍뎅이'
})

console.log(objects);
```
#### 배열 크기 알아내기
``` js
const objects = [{ name: '댕댕' }, { name: '메옹' }];

console.log(objects.length); // 2

objects.push({
  name: '장수풍뎅이'
})

console.log(objects.length); // 3
```
