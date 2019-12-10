# Placeholder hack input[type="date"]
#### 방법 1. ```BEFORE```
``` html
<input type="date" name="inp_date" data-placeholder="등록일" required aria-required="true" />
```
``` css
input[type="date"]::before {
  content: attr(data-placeholder);
  width: 100%
}
input[type="date"]:focus::before,
input[type="date"]:valid::before {display: none}
```
#### 방법 2. ```LABEL```
``` html
<div class="form-date">
  <input type="date" id="inpDate" name="inp_date" required aria-required="true" />
  <label for="inpDate">등록일</label>
<div>
```
``` css
.form-date {position:relative;}
.form-date input {width:100%;height:43px;border:1px solid #d7d7d7;padding-left:10px;font-size:14px;}
.form-date label {position:absolute;left:0;right:0;top:0;bottom:0;}
.form-date input:focus ~ label,
.form-date input:valid ~ label {display:none}
```

- ```required``` 속성 필수. 이 값이 있어야 형식대로 잘 입력 되었을 때 ```placeholder```가 안보이게 된다.
