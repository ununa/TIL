git 재밌다 ㅎㅎㅎㅎㅎ  
++ 으어 너무 바빴다 ㅠㅠ

# git 작업의 흐름

## 01. 로컬 저장소
1. 작업 디렉토리(Working directory): 실제 파일들이 있는 장소
2. 인덱스(Index): 준비 영역
3. HEAD: 최종 확정본(commit)
```
working dir -> add -> Index(Stage) -> commit -> Head
```

#### add 명령어로 index에 추가
```
git add <파일 이름>
git add *
git add --all
```

#### commit 명령어로 확정
```
git commit -m "확정본에 대한 설명"
```


## 02. 변경 내용 발행(Push)
#### 원격 서버의 주소를 git에게 알려주기
```
git remote add origin <원격 저장소 주소>
```
#### 로컬 저장소가 알고있는 원격 origin에 대한 모든 항목을 보여준다.
```
git remote -v
```

#### 변경 내용을 원격 서버로 올리기
```
git push
```
#### 내 저장소의 master 브랜치를 지정
```
git push origin master
```

## 03. 진행 요약
```
git config --global user.name "이름"
git config --global user.email "깃허브 메일주소" // 매번 물어보는 귀찮음을 피하기 위해 설정.

mkdir ~/MyProject   // 로컬 디렉토리 만들고
cd ~/myproject      // 디렉토리로 들어가서
git init            // 깃 명령어를 사용할 수 있는 디렉토리로 만든다.
git status          // 현재 상태를 훑어보고
git add 화일명.확장자  // 깃 주목 리스트에 화일을 추가하고 or
git add .           // 이 명령은 현재 디렉토리의 모든 화일을 추가할 수 있다.
git commit -m “현재형으로 설명” // 커밋해서 스냅샷을 찍는다.

git remote add origin https://github.com/username/myproject.git // 로컬과 원격 저장소를 연결한다.
git remote -v // 연결상태를 확인한다.
git push origin master // 깃허브로 푸시한다.
```

## 04. 원격에서 로컬로(clone)
#### 업데이트 된 코드를 내려 받을 때
```
git pull
```

#### git 소스코드를 로컬로 가져오기.
```
git clone [가져올 원격 저장소 주소]
```

## tip. 
- 커밋 메세지:
https://blog.ull.im/engineering/2019/03/10/logs-on-git.html
- 협업을 위한:
https://nittaku.tistory.com/188
- 집에서(git_home/폴더)
git add f1.txt
git commit f1.txt
git push
- 회사에서 (git_office/ 폴더): git pull 작업이 끝나면 git push 하는 것을 습관화 하기.
git pull
git add f1.txt
git commit f1.txt
git push