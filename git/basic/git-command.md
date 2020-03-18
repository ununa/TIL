# git 명령어
+ git 명령어
- git init
- git status
- git add [파일명 또는 *]
    staging area에 등록
- git commit -m “[설명]”
    repository에 저장
- git config —global user.emal “[이메일]”
- git config —global user.name “[이름]”
- git checkout -b “[브랜치명]”
    브랜치 생성git
- git branch -d [브랜치명]
    브랜치 삭제
- git checkout [브랜치명]
    브랜치 변경
- git branch
    브랜치 목록
- git branch -r
    원격 브랜치 목록
- git checkout -t [remote branch]
- git merge [브랜치명]
    브랜치 병합. 기준이 되는 브랜치로 설정 후 진행해야함
- git diff [브랜치명] [브랜치명]
- git ls-files | xargs wc -l
    해당 프로젝트의 라인 수
- git clone [remote url]
   remote 저장소 가져오기
- git clone -b [branch] https://serverurl
   특정 브런치 remote 저장소 가져오기
- git push origin [브랜치명]
