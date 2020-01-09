# 01. React CDN으로 연결하기
``` html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>React Sample</title>
<script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
</head>
<body>
<script type="text/babel">
ReactDOM.render(
    <h1>Hello, world</h1>,
    document.body
);
</script>
</body>
</html>
```
