# 외부 데이터 사용
웹앱에서 외부 데이터를 다루는 방식은 상당히 표준화 되었다.
```
1. 앱이 원격 서비스에게 데이터를 요청한다.
2. 원격 서비스는 요청을 수신하고 요청된 데이터를 돌려보낸다.
3. 앱이 그 데이터를 받는다.
4. 앱은 받은 데이터를 가공해 사용자에게 보여준다.
```

## 웹 요청에 관한 기초
- ```HTTP```는 브라우저, 또는 그런 종류의 클라이언트와 인터넷의 서버가 통신할 수 있는 공통의 언어를 제공한다.
- 사용자를 대신해 브라우저가 ```HTTP```를 사용해 만드는 요청을 ```HTTP 요청(HTTP request)``` 라고 하며, 그 요청은 새 페이지가 로딩될 때까지 유지된다.

#### 사용자의 정보를 얻기 위한 HTTP 요청: 
```
GET / user
Accept: application/json
```

#### 위 요청에 대한 서버의 응답: 
```
200 OK
Content-Type: application/json

{
  'name': 'Kirupa',
  'url': 'http:https://www.kirupa.com'
}
```
> ```에이잭스(Ajax)```는 페이지를 다시 로딩하지 않고도 비동기식 요청과 데이터 처리를 수행하는 기술이다.  
> 비동기식 자바스크립트와 XML의 줄임말(Asynchronous JavaScript and XML)

#### XMLHttpRequest
자바스크립트에서 HTTP 요청을 보내거나 받는 책임을 지는 객체. 이 객체는 웹 요청을 만듦에 있어 중요한 여러 작업을 한다.
```
1. 서버로 요청을 전송한다.
2. 요청의 상태를 확인한다.
3. 응답을 수신하고 파싱한다.
4. 요청의 상태와 상호작용할 수 있게 하는, readystatechange라는 이벤트를 리스닝한다.
```

## 이제 리액트 시간!
리액트의 주안점은 프레젠테이션 레이어(MVC에서의 'V')인데, 웹 요청을 다루는 것이 주 목적인 리액트 컴포넌트의 내부에 자바스크립트를 작성해 볼 것이다.

### 시작하기
1. 터미널에서 새 프로젝트가 생성될 위치로 이동
2. ```create-react-app ipaddress``` 명령 실행
3. ```./public```, ```./src``` 폴더 안에 있는 모든 파일 삭제하기

#### ./public/index.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <title>IP Address</title>
</head>

<body>
    <div id="container">
        
    </div>
</body>

</html>
```

#### ./src/index.js
``` js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import IPAddressContainer from './IPAddressContainer';

var destination = document.querySelector('#container');

ReactDOM.render(
    <div>
        <IPAddressContainer />
    </div>,
    destination
);
```
> 이 스크립트는 앱의 진입점이며 React, ReactDOM, CSS, IPAddressContainer 컴포넌트를 표준적인 방법으로 참조한다.

#### ./src/index.css
``` css
body {
    background-color: #ffcc00;
}
```

#### ./src/IPAddressContainer.js
``` js
import React, { Component } from 'react';

class IPAddressContainer extends Component {
    render(){
        return(
            <p>Nothing Yet!</p>
        )
    }
}

export default IPAddressContainer;
```

## IP 주소 가져오기
#### ./src/IPAddressContainer.js 수정
> - ```componentDidMount```라는 생명주기 메소드가 호출되면 HTTP 요청이 만들어져 ipinfo.io라는 웹 서비스에 전송된다.  
> - ipinfo 서비스의 응답이 왔다면 ```processRequest``` 함수를 호출해 결과를 처리하면 된다.  
> - 그다음엔 상태에 저장된 IP주소를 참조하게 ```render``` 메소드를 수정한다.
``` js
import React, { Component } from 'react';

var xhr;

class IPAddressContainer extends Component {
  constructor(props, context) {
    super(props, context);

    this.state = {
      ip_address: "..."
    };

    this.processRequest = this.processRequest.bind(this);
  }

  componentDidMount() {
    xhr = new XMLHttpRequest();
    xhr.open("GET", "https://ipinfo.io/json?token=2277ce4bac0347", true);
    xhr.send();

    xhr.addEventListener("readystatechange", this.processRequest, false);
  }

  processRequest() {
    if (xhr.readyState === 4 && xhr.status === 200) {
      var response = JSON.parse(xhr.responseText);

      this.setState({
        ip_address: response.ip
      });
    }
  }

  render() {
    return (
    <div>{this.state.ip_address}</div>
    );
  }
};

export default IPAddressContainer;
```

### 흥미로운 비주얼 만들기

#### ./src/IPAddress.js
``` js
import React, { Component } from 'react';
import './IPAddress.css';

class IPAddress extends Component {
  render(){
    return(
      <div>
        <h1>{this.props.ip}</h1>
        <p>( This is your IP addresss...probably :P )</p>
      </div>
    )
  }
}

export default IPAddress;
```

#### ./src/IPAddress.css
``` css
h1 {
    margin: -15px;
    padding-top: 140px;
    text-align: center;
    font-size: 60px;
    font-family: sans-serif;
}
p {
    text-align: center;
    font-family: sans-serif;
    color: #907400;
}
```

#### ./src/IPAddressContainer.js
> render 메소드 안에 있는 ip라는 속성을 정의하고 ip_address 라는 상태 변수를 설정해 IPAddress 컴포넌트를 호출한다.
``` js
import React, { Component } from 'react';
import IPAddress from './IPAddress';

var xhr;

class IPAddressContainer extends Component {
  constructor(props, context) {
    super(props, context);

    this.state = {
      ip_address: "..."
    };

    this.processRequest = this.processRequest.bind(this);
  }

  componentDidMount() {
    xhr = new XMLHttpRequest();
    xhr.open("GET", "https://ipinfo.io/json?token=2277ce4bac0347", true);
    xhr.send();

    xhr.addEventListener("readystatechange", this.processRequest, false);
  }

  processRequest() {
    if (xhr.readyState === 4 && xhr.status === 200) {
      var response = JSON.parse(xhr.responseText);

      this.setState({
        ip_address: response.ip
      });
    }
  }

  render() {
    return (
    <IPAddress ip={this.state.ip_address}></IPAddress>
    );
  }
};

export default IPAddressContainer;
```

## Tip. 프레젠테이션 대 컨테이너
1. 모양을 다루는 컴포넌트:  
이는 프레젠테이션 컴포넌트(Presentational Component)로 더 잘 알려져 있다.
2. 보이지 않지만 뭔가를 처리하는 컴포넌트:  
예를 들어 라우팅을 하거나 카운터를 증가시키거나 HTTP 요청을 통해 데이터를 가져오는 등의 여러 작업을 한다. (Container Component)
컴포넌트를 잘 다루는 방법에 대한 비법(https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)
