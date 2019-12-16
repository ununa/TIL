# Grid
```Grid```는 수평선과 수직선이 교차해서 이루어진 집합체.

#### 값의 단위
- ```px```: 크기가 고정된 그리드
- ```fr```: 유연한 크기의 그리드.

## Grid 컨테이너
CSS 그리드의 두 가지 주요 요소는 ```wrapper(부모 요소)```와 ```items(자식 요소)```이다.  
부모 요소에 그리드 컨테이너로 지정하면 바로 밑에 있는 모든 자식 요소는 그리드 아이템이 된다.
> ```display: grid```  
> ```display: inline-grid```  

```css
.wrapper {
  display: grid;
}
```
```html
<div class="wrapper>
  <div class="box1">1</div>
  <div class="box2">2</div>
  <div class="box3">3</div>
  <div class="box4">4</div>
  <div class="box5">5</div>
  <div class="box6">6</div>
</div>
```


## Grid 트랙
그리드의 행과 열은 ```grid-template-columns``` 및 ```grid-template-rows``` 프로퍼티로 정의한다.

### 100px의 너비를 가진 세로 열 방향의 트랙 세 개를 생성.
```css
.wrapper {
  display: grid;
  grid-template-columns: 100px 100px 100px;
}
```

- - -

### fr단위 사용하기
그리드 컨테이너에 남아 있는 공간에 따라 일정한 비율로 확장 및 축소되는 단위
```css
.wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
```
> ```grid-template-columns: 2fr 1fr 1fr;```  
> ```grid-template-columns: 500px 1fr 2fr;```  
> 위와 같이 고정된 크기의 트랙과 비율 단위로 지정된 트랙을 섞어서 사용 가능하다.

- - -

### repeat() 표기법으로 트랙 나열
```repeat()```표기법을 사용하여 트랙의 전체 또는 일부분을 반복해서 나열해준다.
> ```grid-template-columns: 1fr 1fr 1fr;```
```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```
> 첫 번째와 마지막 아이템은 ```20px```, 중간 아이템들은 ```1fr``` 크기의 트랙을 4번 반복
```css
.wrapper {
  display: grid;
  grid-template-columns: 20px repeat(4, 1fr) 20px;
}
```
> ```1fr``` 다음 ```2fr``` 크기의 트랙을 3번 반복.
```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr 2fr);
}
```

- - -

### 잠재적 그리고 명시적 그리드
- 명시적 그리드: 직접 정의한 행과 열로 이루어진 그리드  
```grid-template-columns```, ```grid-template-rows``` 
- 잠재적 그리드: 최소 크기 지정
```grid-auto-columns```, ```grid-auto-rows```

```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 200px;
}
```

- - -

### 트랙 크기 조정과 minmax()
> 높이 최소 100px, 최대 auto
```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: minmax(100px, auto);
}
```

## 그리드 라인
그리드 정의는 라인이 아닌 그리드 트랙을 정의하는 것이다. 그러면 그리드는 아이템을 배치할 때 쓸 수 있게 번호가 매겨진 라인을 자동으로 제공한다.
- ```grid-column-start```
- ```grid-column-end```
- ```grid-row-start```
- ```grid-row-end```
<img src="https://mdn.mozillademos.org/files/14761/1_diagram_numbered_grid_lines.png"></img>

### 라인을 이용한 아이템 배치
```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: minmax(100px, auto);
}

.box1 {
  grid-column-start: 1;
  grid-column-end: 4;
  grid-row-start: 1;
  grid-row-end: 3;
}

.box2 {
  grid-column-start: 1;
  grid-row-start: 3;
  grid-row-end: 5;
}

.box10 {
  grid-column-start: 1;
  grid-column-end: 4;
  grid-row-start: 6;
}
```

- - -

### 그리드 셀
그리드에 있는 가장 작은 구성원이며, 개념상 테이블에 있는 셀과 비슷하다.

- - -

### 그리드 영역
아이템은 행 또는 열 방향 어느 쪽으로든 하나 이상의 셀에 걸쳐있을 수 있으며,  
직사사각형이어야 한다. L자 형태의 영역을 생성할 수 없다.

- - -

### 경계 여백
셀 사이의 경계 여백 혹은 간격 (그저 굵은 선처럼 작용함)
> ```grid-column-gap```  
> ```grid-row-gap```

- - -

### 중첩 그리드
중첩된 그리드는 상위 부모 요소의 그리드와 아무런 관계가 없다.

- - -

### 서브 그리드
중첩된 그리드는 부모 요소와 그리드 트랙을 그대로 참고해서 아이템을 배치하게 된다.  
> ```display: subgrid;```  
> 아직 모든 브라우저에서 구현되지 않았고, 표준이 변경될 수 있음

- - -

### z-index를 이용한 아이템 중첩 조정도 가능

- - -

### 그리드와 display: contents
```display: contents```
> "요소 자신은 어떠한 박스도 생성하지 않지만, 대신 포함하고 있는 하위 자식 요소와 가상 요소(pseudo-elements)가 평소처럼 박스를 생성하게 됩니다.
> 그래서 박스 생성과 레이아웃을 구현할 때, 문서의 계층 구조상 해당 요소가 아래 자식 요소와 가상 요소로 대체된것처럼 다루어집니다.
```html
<div class="wrapper">
  <div class="box box1">
    <div class="nested">a</div>
    <div class="nested">b</div>
    <div class="nested">c</div>
  </div>
  <div class="box box2">Two</div>
  <div class="box box3">Three</div>
  <div class="box box4">Four</div>
  <div class="box box5">Five</div>
</div>
```
```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: minmax(100px, auto);
}
.box1 {
  grid-column-start: 1;
  grid-column-end: 4;
  display: contents;
}
```

