# image 버전관리 캐시삭제

### 1. 수정할때마다 네이밍 변경
```
// 수정 전
a.png

// 수정 후
a_v01.png
```

### 2. 파라미터(매개변수)를 파일명 뒤에 붙히는 방법
파일명은 같지만 파라미터 붙이는 방법.
``` css
/* 수정 전 */
.btn-a {backgroud:url('/resource/img/main/a.png')};

/* 수정 후 */
.btn-a {background:url('resource/img/main/a.png?ver=1.0')}
```
