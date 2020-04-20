# box-decoration-break
box-decoration-break 속성은 컬럼 및 줄바꿈시 테두리와 패딩의 방식을 설정한다.

### 
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Sample</title>
<style>
span {
    padding:0 1em;
    border:2px solid;
    background: rgb(231,198,157);
    font-size:24px;
    line-height:2;
}
.ex1 {
    -webkit-box-decoration-break: clone;
    -o-box-decoration-break: clone;
    box-decoration-break: clone;
}
.ex2 {
    -webkit-box-decoration-break: slice;
    -o-box-decoration-break: slice;
    box-decoration-break: slice;
    background-clip: content-box;
}
</style>
</head>
<body>

<div>
    <h2>box-decoration-break: clone:</h2>
    <span class="ex1">CSS<br/>is<br/>easy<br/>to learn</span>
    
    <h2>box-decoration-break: slice (default):</h2>
    <span class="ex2">CSS<br/>is<br/>easy<br/>to learn</span>
</div>

</body>
</html>

```

#### 브라우저 지원:
https://caniuse.com/#feat=css-boxdecorationbreak