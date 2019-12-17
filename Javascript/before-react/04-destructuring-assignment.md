
## 04. 해체 할당
ES6에서 새로 도입된 해체할당(destructuring assignment). 객체나 배열 일부를 쉽게 변수로 해체할 수 있다.
``` js
const developer = {
  firstName: 'Nathan',
  lastName: 'Sebhastian',
  developer: true,
  age: 25,
}

//destructure developer object
const { firstName, lastName } = developer;
console.log(firstName); // returns 'Nathan'
console.log(lastName); // returns 'Sebhastian'
console.log(developer); // returns the object
```
```developer```객체의 ```firstName```과 ```lastName```프로퍼티를 해체하여 새로운 변수인 ```firstName``` 과 ```lastName```에 할당했다.  
만약, ```firstName``` 프로퍼티를 새로운 변수인 ```name```에 할당하고 싶다면 아래와 같이 하면 된다.

``` js
const { firstName:name } = developer;
console.log(name); // returns 'Nathan'
```
해체 할당은 배열에도 적용할 수 있는데, 객체에선 ```key```를 사용했지만, 배열에선 배열 순서대로 대응한다는 점만 다르다.
``` js
const numbers = [1,2,3,4,5];
const [one, two] = numbers; // one = 1, two = 2
```
```,```을 사용하면 중간 인텍스(index)를 건너 뛰고 해체 할당하는 것도 가능하다.
``` js
const [one, two, , four] = numbers; // one = 1, two = 2, four = 4
```

### React에서 어떻게 쓰이나?
React에서는 메서드 안에 ```state```를 해체할당 하는데 자주 쓰인다.
``` js
reactFunction = () => {
  const { name, email } = this.state;
};
```
stateless 함수형 컴포넌트에서도 자주 쓰이고, 
``` js
const HelloWorld = (props) => {
  return <h1>{props.hello}</h1>;
}
```
매개변수를 바로 해체해서 대입할 수 있다.
