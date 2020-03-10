# 리액트 개발 환경 구성

## Create React와의 첫 만남
1. 시작하기 전에 먼저 노드가 설치 되어있는지 확인(https://nodejs.org)
2. 명령창 열기(명령 프롬프트나 터미널)
3. ```npm install -g create-react-app``` 명령 실행
4. 설치 됐으면 프로젝트 만들고 싶은 위치로 이동
5. ```create-react-app helloworld``` 실행
> helloworld라는 프로젝트가 생성 됨
6. ```cd helloworld``` 프로젝트로 들어가서 
7. ```npm start```로 앱을 테스트하기
> 만약 Create React가 npm보다 선호하는 얀(Yarn)이 이미 설치되어 있다면 ```npm start``` 대신 ```yarn start```를 권유하는 메시지가 뜰 수 있다.
8. 프로젝트가 빌드되고 로컬 웹 서버가 구동되면 ```http://localhost:3000/```창이 자동으로 열리며, 프로젝트가 실행되는 모습을 볼 수 있다.

### 무슨 일이 벌어졌나?
- 브라우저에 로딩됐던 파일은 ```public\index.html``` 파일이다.
- ```index.html```을 살펴보면 ```root```라는 값의 id를 가진 엘리먼트에 리액트 앱이 최종적으로 콘텐츠를 출력시키는 장소이다.
- JSX를 포함한 리액트 앱의 콘텐츠는 ```src``` 폴더 안에 있으며, 그중 시작점은 ```index.js```다.
- ```index.js```를 보면 ```import``` 구문들이 있는데 자바스크립트 안에서 일종의 모듈로 취급되며, 모듈이란 앱의 기능을 분리한 작은 조각이다. 따라서 전체를 가져올 필요 없이 꼭 필요한 조각만 가져와 사용할 수 있다.
- ```app.js```에서 흥미로운건 ```export default App```이라는 마지막 라인인데, ```export```라는 명령 다음에 모듈 식별을 위한 프로젝트 이름을 지정했다. 이는 index.js와 같은 다른 파일에서 Appp 모듈을 임포트할 때 사용될 이름이다.
- 빌드 과정은 임포트하는 모든 파일과 컴포넌트가 부라우저가 감당할 수 있는 조합된 파일들로 만들어 준다. 즉, 최종적으로는 관련된 조각들이 합쳐진 하나의 js 파일이 만들어진다.

## HelloWorld 앱 개발
### 1. 시작
- ```./src```에 있는 기존 파일 삭제
- ```index.js```, ```HelloWorld.js``` 빈 파일 추가
> 앱이 꺼졌다면 명령창에서 ```Ctrl+C```를 눌러 세션을 중단한 뒤 해당 프로젝트 위치에서 ```npm start``` 명령 입력하면 실행된다.

#### index.js
``` js
import React from 'react';
import ReactDOM from 'react-dom';
import HelloWorld from './HelloWorld';
import './index.css';

ReactDOM.render(
    <HelloWorld />,
    document.getElementById('root')
);
```

#### HelloWorld.js
``` js
import React, { Component } from 'react';
import './HelloWorld.css';

class HelloWorld extends Component {
    render(){
        return(
            <div className="helloContainer">
                <h1>Hello, world!</h1>
            </div>
        );
    }
}

export default HelloWorld;
```
### 2. 스타일 입히기
- ```index.css```, ```HelloWorld.css``` 파일 추가
> HelloWorld 컴포넌트만을 위한 새 CSS를 따로 만든 이유는 관련된 파일을 그룹화하여 진행하기 위함이다.

#### index.css
``` css
body {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  margin: 0;
}
```

#### HelloWorld.css
``` css
h1 {
  padding:5px 15px;
  margin: 0;
  background: linear-gradient(to bottom, white 0%, white 62%, gold 62%, gold 100%);
  font-size: 56px;
  font-family: sans-serif;
}
```

## 운영 버전 빌드하기
지금까지의 개발 모드에서 앱을 빌드해왔다. 하지만 앱을 실제 사용자에게 공개하려면 더 빠르면서도 가장 작게 만들기 위해 해법이 필요하다.
### 빌드하기
- ```Ctrl+C```를 눌러 세션을 중단하고 ```npm run build``` 명령을 실행
- 빌드가 완료되면 서버에 배포하거나 ```serve```라는 노드 패키지를 사용해 로컬에서 테스트 할 수 있다는 안내를 볼 수 있다.


