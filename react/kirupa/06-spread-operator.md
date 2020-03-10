# 속성 전달
- 속성을 전달 할 때 중간 계층을 건너뛸 수 없다.
- 자식으로부터 부모로 속성을 거꾸로 올려 보낼 수도 없다.
- 모든 소통은 부모로부터 직계 자식에게 일방적으로만 이뤄진다.
- 이는 리액트의 작동 원리에 기인하며, 리액트는 반드시 부모 컴포넌트에서 직계 자식 컴포넌트로만 속성이 내려가게 하는 연쇄적인 명령 실행만 가능하다.

### 속성 전달 예제 코드
``` js
class Display extends React.Component {
    render(){
        return(
            <div>
                <p>{this.props.color}</p>
                <p>{this.props.num}</p>
                <p>{this.props.size}</p>
            </div>
        );
    }
}

class Label extends React.Component {
    render(){
        return(
            <Display color={this.props.color}
                     num={this.props.num}
                     size={this.props.size} />
        );
    }
}

class Shirt extends React.Component {
    render(){
        return (
            <Label  color={this.props.color}
                    num={this.props.num}
                    size={this.props.size}/>
        );
    }
}

ReactDOM.render(
    <div>
        <Shirt color="steelblue" num="3.14" size="medium" />
    </div>,
    document.querySelector('#container')
)

```

## 스프레드 연산자와의 만남
- ```...``` : 스프레드 연산자(또는 전개 연산자 spread operator)
- 스프레드 연산자는 배열 안의 개별 요소를 밖으로 풀어내는 역할을 한다.
#### 스프레드 예제 
``` js
var items = [1, 2, 3];

function printStuff(a, b, c) {
  console.log('printing: ' + a + " " + b + " " + c);
}

// 스프레드 연산자 사용
printStuff(...items);

// 스프레드 연산자 미사용
printStuff(items[0], items[1], items[2]);
```

## 더 나은 속성 전달 방법
``` js
class Display extends React.Component {
    render(){
        return(
            <div>
                <p>{this.props.color}</p>
                <p>{this.props.num}</p>
                <p>{this.props.size}</p>
            </div>
        );
    }
}

class Label extends React.Component {
    render(){
        return(
            <Display {...props} /> // 스프레드 연산자 사용
        );
    }
}

class Shirt extends React.Component {
    render(){
        return (
            <Label {...props} /> // 스프레드 연산자 사용
        );
    }
}
```
- 실행 결과는 이전과 같지만, 컴포넌트를 호출할 때 각 속성을 일일이 풀어서 전달할 필요가 없다.
- 단, 특정 컴포넌트로 속성을 전달하는 게 하고자 하는 일의 전부라면 불필요한 각 중간 컴포넌트들이 전달자 역할을 해야 하기 때문에 완벽한 해법은 아니다.
- 어떤 속성의 변경이라도 그 속성을 전달하는 모든 컴포넌트들까지 갱신 작업이 일어나기 때문에 성능 저하의 가능성도 있다.


