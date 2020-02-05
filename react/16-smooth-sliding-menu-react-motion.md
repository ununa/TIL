# 슬라이드 메뉴
> 예제 링크: https://www.kirupa.com/react/examples/slidingmenu_css/index.html

## 슬라이드 메뉴의 작동 원리
1. 슬라이드 메뉴의 정확한 작동 원리를 이해해보자.
2. 메뉴는 콘텐츠 화면의 왼쪽에 존재하며, 호출되기 전까지는 그 자리에서 대기 하고 있다.
3. 화면 안으로 들어오라는 호출을 받으면 메뉴를 브라우저 창의 원래 위치까지 오른쪽으로 이동시키면 된다.

## 개발 준비
1. ```MenuContainer``` 컴포넌트 : 가장 상위에 위치. 역할은 상태 관리 등의 비시각적 기능을 수행하고, Menu와 MenuButton 컴포넌트를 호스팅하며, 초기 텍스트를 화면에 보여주는 일이다.

## 시작하기
``` create-react-app slidingmenu```

#### ./public/index.html
``` html
<!DOCTYPE html>
<html>

<head>
    <title>Sliding Menu in React</title>
</head>

<body>
    <div id="container"></div>
</body>

</html>
```

#### ./src/index.js
``` js
import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import MenuContainer from "./MenuContainer";

ReactDOM.render(
    <MenuContainer/>,
    document.querySelector("#container")
);
```

#### ./src/index.css
``` css
body {
    overflow: auto;
    padding: 25px;
    margin: 0;
    background-color: #eee;
    font-size: 20px;
    font-family: sans-serif;
}

#container li {
    margin-bottom: 10px;
}
```

#### ./src/MenuContainer.js
``` js
import React, { Component } from "react";

class MenuContainer extends Component {
    render(){

        return(
            <div>
                <div>
                    <p>Can you spot the item that doesn't belong?</p>
                    <ul>
                        <li>Lorem</li>
                        <li>Ipsum</li>
                        <li>Dolor</li>
                        <li>Sit</li>
                        <li>Bumblebees</li>
                        <li>Aenean</li>
                        <li>Consectetur</li>
                    </ul>
                </div>
            </div>
        );
    }
}

export default MenuContainer;
```

## 메뉴 보이기와 감추기
```
1. 버튼을 클릭하면 슬라이드 메뉴가 화면에 나타난다.
2. 아무 곳이나 클릭하면 슬라이드 메뉴는 화면 밖으로 다시 사라진다.
```
#### 조건
- 메뉴가 보이고 있는지 숨겨져 있는지를 추적할 수 있는 상태를 관리해야 한다.
- 이 상태는 버튼이나 메뉴가 클릭되면 갱신돼야 한다.
- 또한 상태 메뉴와 버튼이 모두 접근할 수 있는 공통 위치에 존재해야 한다.
- 그 공통 위치는 MenuContainer 컴포넌트의 내부가 적당할 것이므로, 이 컴포넌트에 상태 관련 로직을 추가해야한다.


#### ./src/MenuContainer.js
``` js
    // render 메소드 위에 생성자와 toggleMenu 메소드 추가
    constructor(props) {
        super(props);

        this.state = {
            visible: false
        }
        this.handleMouseDown = this.handleMouseDown.bind(this);
        this.toggleMenu = this.toggleMenu.bind(this);
    }

    handleMouseDown(e){
        this.toggleMenu();

        console.log('checked');
        e.stopPropagation();
    }

    toggleMenu(){
        this.setState({
            visible: !this.state.visible
        });
    }
```

- ```visible```이라는 변수를 상태 객체에 저장했음
- ```visible```의 값을 true나 false로 전환해줄 ```toggleMenu```라는 메소드를 만들었다.
- ```handleMouseDown``` 메소드가 호출되면 메뉴를 토글할 ```toggleMenu```가 호출 됨

### 버튼 제작
```
- MenuButton.js
- MenuButton.css
```
- ```MenuButton 컴포넌트```에 ```handleMouseDown```이라는 속성을 전달
- 그 속성의 값은 앞서 정의했던 ```handleMouseDown```이라는 이벤트 핸들러다.
- 이렇게 함으로 ```MenuButton 컴포넌트``` 안의 버튼이 클릭되면 ```MenuContainer 컴포넌트``` 안의 ```handleMouseDown``` 메소드가 호출하게 된다.

#### ./src/MenuButton.css
``` css
#roundButton {
  background-color: #96D9FF;
  margin-bottom: 20px;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border: 10px solid #0065A6;
  outline: none;
  transition: all .2s cubic-bezier(0, 1.26, .8, 1.28);
}
 
#roundButton:hover {
  background-color: #96D9FF;
  cursor: pointer;
  border-color: #003557;
  transform: scale(1.2, 1.2);
}
 
#roundButton:active {
  border-color: #003557;
  background-color: #FFF;
}
```

#### ./src/MenuButtons.js
``` js
import React, { Component } from "react";
import "./MenuButton.css";

class MenuButton extends Component {
    render(){

        return (
            <button
                id="roundButton"
                onMouseDown={this.props.handleMouseDown}
            >
            </button>
        );
    }
}

export default MenuButton;
```

#### ./src/MenuContainer.js
``` js
import MenuButton from "./MenuButton";
    .
    .
    .

render(){
    return(
        <div>
        <MenuButton handleMouseDown={this.handleMouseDown}/>
        .
        .
        .
    );
}
```

### 메뉴 제작
메뉴와 관련된 모든 사항을 책임질 Menu 컴포넌트를 만들어야 한다.

#### ./src/MenuContainer.js
``` js
import Menu from "./Menu";
    .
    .
    .

render(){
    return(
        <div>
        <MenuButton handleMouseDown={this.handleMouseDown}/>
        <Menu handleMouseDown={this.handleMouseDown}
            menuVisibility={this.state.visible} />
        .
        .
        .
    );
}
```

#### ./src/Menu.css
``` css
#flyoutMenu {
  width: 100vw;
  height: 100vh;
  background-color: #FFE600;
  position: fixed;
  top: 0;
  left: 0;
  transition: transform .3s
              cubic-bezier(0, .52, 0, 1);
  overflow: scroll;
  z-index: 1000;
}
 
#flyoutMenu.hide {
  transform: translate3d(-100vw, 0, 0);
}
 
#flyoutMenu.show {
  transform: translate3d(0vw, 0, 0);
  overflow: hidden;
}
 
#flyoutMenu h2 a {
  color: #333;
  margin-left: 15px;
  text-decoration: none;
}
 
#flyoutMenu h2 a:hover {
  text-decoration: underline;
}
```

#### ./src/Menu.js
``` js
import React, { Component } from "react";
import "./Menu.css";

class Menu extends Component {
    render(){
        var visibility = "hide";

        if (this.props.menuVisibility) {
            visibility = "show";
        }

        return (
            <div id="flyoutMenu"
                onMouseDown={this.props.handleMouseDown}
                className={visibility} >
                <h2><a href="/">HOME</a></h2>
                <h2><a href="/">ABOUT</a></h2>
                <h2><a href="/">CONTACT</a></h2>
                <h2><a href="/">SEARCH</a></h2>
            </div>
        );
    }
}

export default Menu;
```
- ```<Menu handleMouseDown ...>``` : 속성과 이벤트 핸들러 값
- ```<Menu ... menuVisibility>``` : visible이라는 상태 속성의 현재 값
- ```<div id="flyoutMenu">