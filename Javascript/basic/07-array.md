## 07. 배열
객체는 한 변수 혹은 상수에 여러가지 정보를 담기 위함이었다면,  
배열은 여러개의 항목들이 들어있는 리스트와 같다.

배열(array)이라는 타입은 없으며, **배열 또한 객체**인 것이다.  
배열에는 순서가 있다. (index)

배열은 대괄호(```[ ]```)를 이용해 선언하며, 각 배열의 요소는 콤마를 이용해 구분하고  
배열의 각 항목에는 어떠한 자료형의 값이 와도 상관 없다.

### 배열 사용하기
#### 비어있는 배열 선언
``` js
const array = [];
```
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
첫 번째 인텍스는 0 부터 시작.

``` js
const objects = [{ name: '댕댕' }, { name: '메옹' }];

console.log(objects);
console.log(objects[0]); //=> { name: '댕댕' }
console.log(objects[1]); //=> { name: '메옹' }
```
#### 배열 추가
배열이 지니고 있는 내장 함수 ```push``` 함수를 사용 (스택 자료구조)
``` js
const objects = [{ name: '댕댕' }, { name: '메옹' }];

objects.push({
  name: '장수풍뎅이'
})

console.log(objects);
```
#### 배열 크기 알아내기
```length``` 프로퍼티를 이용해서 알 수 있다.
``` js
const objects = [{ name: '댕댕' }, { name: '메옹' }];

console.log(objects.length); // 2

objects.push({
  name: '장수풍뎅이'
})

console.log(objects.length); // 3
```
