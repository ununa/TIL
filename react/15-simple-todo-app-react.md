# Todo List 앱 제작
링크: https://www.kirupa.com/react/examples/todo.htm

## 시작하기
### 1. 터미널에서 새 프로젝트를 만들자.  
``` create-react-app todolist```
### 2. 기본세팅
#### ./public/index.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <title>Todo List</title>
</head>

<body>
    <div id="container">
        
    </div>
</body>

</html>
```

#### ./src/index.css
``` css
body {
    padding: 50px;
    background-color: #66ccff;
    font-family: sans-serif;
}
#container {
    display: flex;
    justify-content: center;;
}
```

#### ./src/index.js
``` js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';

var destination = document.querySelector('#container');

ReactDOM.render(
    <div>
        <p>Hello!</p>
    </div>,
    destination
);
```

## 초기 UI 제작
#### ./src/TodoList.js 추가
``` js
import React, { Component } from "react";


class TodoList extends Component{
    render() {
        return(
            <div className="todoListMain">
                <div className="header">
                    <form>
                        <input placeholder="enter task"></input>
                        <button type="submit">add</button>
                    </form>
                </div>
            </div>
        );
    }
}

export default TodoList;
```

#### index.js 수정
``` js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import TodoList from './TodoList'; // 추가

var destination = document.querySelector('#container');

ReactDOM.render(
    <div>
        <TodoList /> // 수정
    </div>,
    destination
);
```

## 앱의 나머지 부분 개발
모든 비주얼과 데이터를 함께 묶는게 진짜 일인데, 이 작업은 다음과 같은 대략 다섯 가지 부분으로 나눌 수 있다.
```
1. 아이템 추가
2. 아이템 표시
3. 스타일 적용
4. 아이템 삭제
5. 아이템 추가와 삭제 시 애니메이션 적용
```

### 1. 아이템 추가
첫 번째로 해야 할 주된 작업은 이벤트 핸들러와 기본 폼 핸들러를 설정해 아이템이 추가 될 수 있게 하는 일이다.
#### ./src/TodoList.js
> - 폼에서 submit 이벤트를 리스닝
> - 이벤트가 발생하면 addItem 메소드를 호출
``` js
import React, { Component } from "react";

class TodoList extends Component{
    render() {
        return(
            <div className="todoListMain">
                <div className="header">
                    <form onSubmit={this.addItem}> // onSubmit 추가
                        <input placeholder="enter task"></input>
                        <button type="submit">add</button>
                    </form>
                </div>
            </div>
        );
    }
}

export default TodoList;
```

#### ./src/TodoList.js
> - ```state``` 객체엔 사용자가 입력하는 아이템을 저장할 배열인 items라는 속성 하나를 정의함.
> - ```ref```를 통해 사용자가 제출 버튼을 누르면 input 엘리먼트로부터 값을 읽어 items에 저장하게 한다.
> - ref는 DOM에 접근하기 위한 관문을 제공한다.
> - ```_inputElement```속성: input 엘리먼트의 참조를 저장한다.
> - ```ref={(a) => this._inputElement = a}```: 이 컴포넌트 안의 input 엘리먼트에 접근하고 싶으면 _inputElement를 통해 할 수 있다.
> - ```addItem``` 함수
> - ```var itemArray = this.state.items;```: 상태 객체에 있는 items의 현재 값을 저장하기 위해 만든 변수
> - ```if (this._inputElement.value !== "") {...}```: input 엘리먼트 안에 콘텐츠가 있는지 확인하고, 만약 비어 있다면 아무 일도 하지 않지만 텍스트가 들어있다면 그 텍스트를 ```itemArray```에 추가한다.
> - ```(Date.now())```: 현재 시간을 키 값으로 두었다.
> - ```e.preventDefault();```: 기본 동작 막기. 사용자가 폼을 제출하면 기본적으로 페이지는 다시 로딩되며 모든 사항이 초기화 되지만 preventDefault를 호출함으로써 그런 기본 동작을 막았다.
``` js
import React, { Component } from "react";


class TodoList extends Component{
    constructor(props) {
        super(props);

        this.state = {
            items: []
        }

        this.addItem = this.addItem.bind(this);
    }

    addItem(e) {
        var itemArray = this.state.items;

        if (this._inputElement.value !== "") {
            itemArray.unshift({
                text: this._inputElement.value,
                key: Date.now()
            });

            this.setState({
                items: itemArray
            });

            this._inputElement.value = "";
        }

        console.log(itemArray);

        e.preventDefault();
    }

    render() {
        return(
            <div className="todoListMain">
                <div className="header">
                    <form onSubmit={this.addItem}>
                        <input  ref={(a) => this._inputElement = a}
                                placeholder="enter task">        
                        </input>
                        <button type="submit">add</button>
                    </form>
                </div>
            </div>
        );
    }
}

export default TodoList;
```

### 2. 아이템 표시
- TodoItems 새로운 컴포넌트 만들기
- items 배열을 속성으로 전달하기

#### ./src/TodoList.js
``` js
import React, { Component } from "react";
import TodoItems from './TodoItems'; // 추가
import './TodoList.css'; // 추가
.
.
.

    render() {
        return(
            <div className="todoListMain">
                <div className="header">
                    <form onSubmit={this.addItem}>
                        <input  ref={(a) => this._inputElement = a}
                                placeholder="enter task">        
                        </input>
                        <button type="submit">add</button>
                    </form>
                </div>
                <TodoItems entries={this.state.items} /> // 추가
            </div>
        );
    }
```

#### ./src/TodoItems.js 추가
> - ```render``` 함수에서는 ```entries``` 속성을 통해 '할 일' 아이템을 받아 JSX와 HTML식 코드로 바꾼다. 이를 위해서 createTasks와 map 함수를 사용했다.
> - ```listItems``` 변수에 저장된 값은 화면에 출력할 콘텐츠를 담고 있는 li 엘리먼트의 배열이다. 여기서 key 속성의 값(앞서 봤던 Date.now())을 각 엘리먼트에 설정함으로써 리액트가 엘리먼트 추적을 쉽게 할 수 있었다.

``` js
import React, { Component } from 'react';

class TodoItems extends Component {
    createTasks(item) {
        return <li key={item.key}>{item.text}</li>
    }

    render(){
        var todoEntries = this.props.entries;
        var listItems = todoEntries.map(this.createTasks);

        return(
            <ul className="theList">
                {listItems}
            </ul>
        )
    };
}

export default TodoItems;
```

#### ./src/TodoList.css 추가
``` css
.todoListMain .header input {
  padding: 10px;
  font-size: 16px;
  border: 2px solid #FFF;
  width: 165px;
}
.todoListMain .header button {
  padding: 10px;
  font-size: 16px;
  margin: 10px;
  margin-right: 0px;
  background-color: #0066FF;
  color: #FFF;
  border: 2px solid #0066FF;
}
.todoListMain .header button:hover {
  background-color: #003399;
  border: 2px solid #003399;
  cursor: pointer;
}
.todoListMain .theList {
  list-style: none;
  padding-left: 0;
  width: 250px;
} 
.todoListMain .theList li {
  color: #333;
  background-color: rgba(255,255,255,.5);
  padding: 15px;
  margin-bottom: 15px;
  border-radius: 5px;
  list-style: none;
}
ul.theList {
  padding: 0;
}

.todoListMain .theList li {
  color: #333;
  background-color: rgba(255,255,255,.5);
  padding: 15px;
  margin-bottom: 15px;
  border-radius: 5px;

  transition: background-color .2s ease-out;
}

.todoListMain .theList li:hover {
  background-color: pink;
  cursor: pointer;
}
```

### 3. 아이템 삭제
- 클릭 할 아이템은 TodoItems.js에 정의 되어 있고, state 객체에 아이템을 채우는 실제 로직은 TodoList.js에 있다.
- 따라서 이 두 컴포넌트 사이에 뭔가를 전달하기 위한 기법을 사용해보자.

####  ./src/TodoItems.js 수정
> - 단순히클릭이벤트를리스닝하며,이를delete라고 하는 이벤트 핸들러에 연결했다.
``` 
    createTasks(item) {
        return <li onClick={() => this.delete(item.key)} 
                   key={item.key}>{item.text}</li>
    }
```

#### ./src/TodoItems.js
> - ```delete``` 이벤트 핸들러 정의: ```key```를 인자로 받는 ```delete```라는 함수를 정의했다. 또한 생성자를 추가해 그 안에서 ```this```를 명시적으로 바인딩 했다.
> - 그러나 ```delete``` 함수가 실제로 삭제 작업을 하지 않고 속성을 통해 ```this``` 컴포넌트에 전달된 또 다른 ```delete``` 함수를 호출한다.
``` js
class TodoItems extends Component {
    constructor(props) {
        super(props);

        this.createTasks = this.createTasks.bind(this);
    }

    delete(key) {
        this.props.delete(key);
    }
````

#### ./src/TodoList.js
> - ```TodoItems```를 호출하는 부분에서 ```delete```라는 속성을 추가하고 ```deleteItem``` 함수를 지정함.
> - 이렇게 하면 ```TodoItems``` 컴포넌트는 ```delete```라는 속성을 인지하게 되며, 이는 ```TodoList```에 추가할 삭제 함수를 실제로 연결시킨다는 의미이다.
``` js
    render() {
        return(
            <div className="todoListMain">
                <div className="header">
                    <form onSubmit={this.addItem}>
                        <input  ref={(a) => this._inputElement = a}
                                placeholder="enter task">        
                        </input>
                        <button type="submit">add</button>
                    </form>
                </div>
                <TodoItems entries={this.state.items}
                           delete={this.deleteItem}/> // 추가
            </div>
        );
    }
```

#### ./src/TodoList.js
> - ```deleteItem(){}``` 함수 추가
> - 클릭된 아이템으로부터의 ```key```를 ```filter``` 메소드로 전달해 현재 저장하고 있던 ```key```와 비교한다.
> - 삭제될 아이템을 제외한 모든 아이템을 갖는 ```filteredItems```라는 새로운 배열이 만들어지며, 이 배열은 다시 ```state``` 객체의 ```items``` 속성에 지정 된다.
``` js
    deleteItem(key) {
        var filteredItems = this.state.items.filter(function (item) {
            return (item.key !== key);
        });
       
        this.setState({
            items: filteredItems
        });
    }
```

#### ./src/TodoList.js
> - UI가 갱신되고 해당 아이템은 사라지며, 마지막으로 this에 대한 통상적인 바인딩 작업을 해야한다.
> - ```deleteItem``` 안의 ```this``` 는 올바른 참조를 갖게 되며, 이로써 아이템 삭제 기능을 완전히 구현했다.
``` js
    constructor(props) {
        super(props);

        this.state = {
            items: []
        }

        this.addItem = this.addItem.bind(this);
        this.deleteItem = this.deleteItem.bind(this);
    }
```

## 애니메이션
- 플립 무브(Flip Movoe): 경량의 애니메이션 라이브러리
- 터미널을 열어 현재 위치가 todolist 프로젝트 폴더임을 확인한 뒤 
- ```npm i -S react-flip-move``` 명령 실행
- 이렇게 하면 프로젝트의 node_modules 폴더 안에 복사될 것이다.

#### TodoItems.js 
``` js
import FlipMove from 'react-flip-move'; // 추가
.
.
.
        return(
            <ul className="theList">
                <FlipMove duration={250} easing="ease-out"> // 추가
                    {listItems}
                </FlipMove>
            </ul>
        )
    };
}
```
### .
### .
### .
### 최종 코드
#### TodoList.js
``` js
import React, { Component } from "react";
import TodoItems from './TodoItems';
import './TodoList.css';


class TodoList extends Component{
    constructor(props) {
        super(props);

        this.state = {
            items: []
        }

        this.addItem = this.addItem.bind(this);
        this.deleteItem = this.deleteItem.bind(this);
    }

    addItem(e) {
        var itemArray = this.state.items;

        if (this._inputElement.value !== "") {
            itemArray.unshift({
                text: this._inputElement.value,
                key: Date.now()
            });

            this.setState({
                items: itemArray
            });

            this._inputElement.value = "";
        }
        console.log(itemArray);

        e.preventDefault();
    }

    deleteItem(key) {
        var filteredItems = this.state.items.filter(function (item) {
            return (item.key !== key);
        });
       
        this.setState({
            items: filteredItems
        });
    }

    render() {
        return(
            <div className="todoListMain">
                <div className="header">
                    <form onSubmit={this.addItem}>
                        <input  ref={(a) => this._inputElement = a}
                                placeholder="enter task">        
                        </input>
                        <button type="submit">add</button>
                    </form>
                </div>
                <TodoItems entries={this.state.items}
                           delete={this.deleteItem}/>
            </div>
        );
    }
}

export default TodoList;
```

#### TodoItems.js
``` js
import React, { Component } from 'react';
import FlipMove from 'react-flip-move';


class TodoItems extends Component {
    constructor(props) {
        super(props);

        this.createTasks = this.createTasks.bind(this);
    }

    delete(key) {
        this.props.delete(key);
    }

    createTasks(item) {
        return <li onClick={() => this.delete(item.key)} 
                   key={item.key}>{item.text}</li>
    }

    render(){
        var todoEntries = this.props.entries;
        var listItems = todoEntries.map(this.createTasks);

        return(
            <ul className="theList">
                <FlipMove duration={250} easing="ease-out">
                    {listItems}
                </FlipMove>
            </ul>
        )
    };
}

export default TodoItems;
```
