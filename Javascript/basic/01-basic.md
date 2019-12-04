
# Object Model
``` js
var imgs = document.getElementsByTagName('img'); // 복수의 태그 목록
imgs[0]
```

### BOM(Browser Object Model)
웹페이지의 내용을 제외한 브라우저의 각종 요소들을 객체화시킨 것. 전역객체 ```window```의 프로퍼티에 속한 객체들이 이에 속한다.
``` html
<input type="button" onclick="alert(window.location)" value="alert(window.location)" />
<input type="button" onclick="window.open('bom.html')" value="window.open('bom.html')" />
```

### DOM(Document Object Model)
```window```의 프로퍼티인 ```document```프로퍼티에 할당된 ```document```객체가 이러한 작업을 담당.  
문서 내의 주요 엘리먼트에 접근할 수 있는 객체를 제공함.
``` html
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
<script>
    // body 객체
    console.log(document.body);
    // 이미지 객체들의 리스트
    console.log(document.images);
      // body 객체
    console.log(document.getElementsByTagName('body')[0]);
    // 이미지 객체들의 리스트
    console.log(document.getElementsByTagName('body'));
</script>
```
