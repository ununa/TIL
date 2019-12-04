# 이벤트
### 시작점
#### jQuery
``` js
$.ready(() => {
  // code...
})
```

#### JavaScript
``` js
document.addEventListener('DOMContentLoaded', () => {
  // code...
})
```
HTML을 파싱한 뒤 DOM 객체를 생성이 완료되면 ```DOMContentLoaded``` 이벤트가 발생한다.


### 클릭 이벤트
#### jQuery
``` js
$('a').on('click', evt => {
  // event code...
})

// emit: 기본 이벤트
$('a').click()

// emit: 커스텀 이벤트
$('a').trigger('@click')
```

#### JavaScript
``` js
document.querySelector('a').addEventListener('click', event => {
  // HTML을 파싱한 뒤 DOM 객체를 생성이 완료되면 'DOMContentLoaded' 이벤트가 발생한다.
});

// emit: 기본 이벤트 (똑같은 click() 함수를 사용함)
document.querySelector('a').click();

// emit: 커스텀 이벤트 CustomEvent 클래스로 이벤트 객체를 만들고 document.dispatchEvent() 함수로 이벤트를 방출
const evt = new CustomEvent('@click');
document.dispatchEvent(evt)

// 이벤트 + 데이터
const evt = new CustomEvent('@click', {detail: 'some data'})
document.dispatchEvent(evt)

// CustormEvent 생성시 두번째 인자로 detail 키를 갖는 객체만 넘겨주고 사용하기
// IE11
document.querySelector('a').addEventListener('@click', evt => {
  evt.detail // 'some data'
})
// ~ IE11
const evt = document.createEvent('CustomEvent');
evt.intiCustomEvent('@click', true, false, 'some data')
document.dispatchEvent(evt)
```
- ```document.createEvent()``` 함수로 생성한 이벤트 객체의 ```initCustomEvent()``` 함수로 이벤트 명과 전달할 데이터를 설정
- 매개변수는 순서대로 이벤트명, 버블(bubble), 취송가능여보(cancelable), 전달할 데이터(detail)의미함
