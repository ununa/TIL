# jQuery 보다 먼저 알았으면 좋았을 것들.

## 돔(DOM) 선택
#### HTML
``` html
<div id="app" class="container" data-product-id="G123">Guitar</div>
```

#### jQuery
``` js
// id
$('#app')

// class
$('.container')

// data
$('div').data('product-id')

```

#### JavaScript
``` js
// id
document.getElementById('app') // ID로 돔을 찾는 방식
document.querySelector('#app') // CSS 스타일 선택자

// class
document.getElementsByClassName('container') // 전부 반환 => 1
document.querySelector('.container') // 첫 번째만 반환 => undefined
document.querySelectorAll('.container') // 전부 반환 => 1

// data
// dataset. IE11 미만 지원x
document.querySelector('div').dataset.productId // 'G123'
document.querySelector('div').dataset.productId = 'G456' // 속성 값 변경.

// getAttribute(), setAttribute()
document.querySelector('div').getAttribute('data-product-id') // 'G123'
```
