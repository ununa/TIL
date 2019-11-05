## 04. 조건문

조건문을 사용하면 특정 조건이 만족됐을 때 특정 코드를 실행

### if문
"~~하다면 ~~를 해라" 를 의미
``` js
if (조건) {
  코드;
}
```

### if-else문
"~~하다면 ~~하고, 그렇지 않다면 ~~해라." 를 의미
``` js
const a = 10;
if (a > 15) {
  console.log('a 가 15 큽니다.');
} else {
  console.log('a 가 15보다 크지 않습니다.');
}

// "a 가 10보다 크지 않습니다."
```


### if-else if 문
여러 조건에 따라 다른 작업을 해야 할 때 사용
``` js
const a = 10;
if (a === 5) {
  console.log('5입니다!');
} else if (a === 10) {
  console.log('10입니다!');
} else {
  console.log('5도 아니고 10도 아닙니다.');
}

// "10입니다!"
```

### switch/case 문  
특정 값이 무엇이냐에 따라 다른 작업을 하고 싶을 때 사용
``` js
const device = 'iphone';

switch (device) {
  case 'iphone':
    console.log('아이폰!');
    break;
  case 'ipad':
    console.log('아이패드!');
    break;
  case 'galaxy note':
    console.log('갤럭시 노트!');
    break;
  default:
    console.log('모르겠네요..');
}

```
switch/case 문에서는 각 case 에서 실행할 코드를 작성하고 맨 마지막에 ```break;``` 를 해야함.
break 를 하지 않으면 그 다음 ```case``` 의 코드까지 실행해버림.
맨 아래의 ```default:``` 는 device 값이 case에 속하지 않은 값일 경우를 의미.
