# git, github 버전관리

## 깃설치, 깃허브 레포지토리 만들기

- 깃설치 https://git-scm.com/download/win 64bit버전 설치
- use visual studio code as git's default editor 깃 기본에디터 변경

---

- github 회원가입

- 프로젝트명 기반으로 원격레포지토리(보관소) 만들기: github > 레포지토리 > new
  
  ex. next13-share-prompts, react-todo

- git add . 모든변경사항 스테이징(vscode 소스제어 > 변경사항 +클릭)

- LF -> CRLF 경고(시스템별 줄바꿈문자열이 달라 나오는 경고) 나오면 git config --global core.autocrlf true

- LF -> CRLF 경고 계속 뜨는경우(편집기때문) git config --global core.safecrlf false

---

## 이슈 템플릿 설정

- 깃헙 > settings > Features - Issues, Set up templates 이슈템플릿 설정

- Add template - Custom template - Preview and edit

- Template name: 이슈 템플릿, About: 작업이슈 만들때 사용

- Template content: #개요 ##요구사항

- Propose changes - commit 메세지: update issue templates

- commit하면 .github/ISSUE_TEMPLATE 폴더 생성

- 이슈 생성시 Assignees(관련 팀원), Labels(이슈종류), Projects 를 설정

---

## 커밋템플릿작성 및 연결

- ni ~/.gitmessage.txt c:\Users\윈도우사용자계정에 파일만든후 vscode로 열고 커밋샘플메세지 복붙

```textile
################
# 타입: 제목 #이슈번호 형식으로 제목을 아래 공백줄에 작성
# 제목은 50자 이내 / 변경사항이 "무엇"인지 명확히 작성 / 끝에 마침표 금지
# 예) feat: 로그인 기능 추가 #이슈번호, feat: nextjs13 프로젝트 시작, feat: 메인 UI 적용 #이슈번호

# 바로 아래 공백은 지우지 마세요 (제목과 본문의 분리를 위함)

################
# 본문(구체적인 내용)을 아랫줄에 작성
# 여러 줄의 메시지를 작성할 땐 "-"로 구분 (한 줄은 72자 이내)

################
# feat: 새로운 기능 추가
# fix: 버그 수정
# docs: 문서 수정
# test: 테스트 코드 추가
# refact: 코드 리팩토링
# style: 코드 의미에 영향을 주지 않는 변경사항
# chore: 빌드 부분 혹은 패키지 매니저 수정사항
################
```

- git config --global commit.template ~/.gitmessage.txt 커밋템플릿연결

---

## 깃헙 계정정보 설정

- git config --global user.email "dalhoya@naver.com"
- git config --global user.name "ossamuiux"

---

## git commit

- 커밋메세지 작성후 저장하고 닫으면 로컬저장소에 커밋
- 원격저장소 추가: git remote add origin 원격저장소주소, origin은 원격저장소 이름
- 인증화면에서 사용자인증
- git push origin master, 원격저장소(origin) master 브랜치에 업로드

---

## PR(풀리퀘스트) 깃헙 세팅

- 동일 레포지토리에서 다른 팀원과 협업시 push후 PR을 통해 주브랜치에 머지하고 다른 팀원들이 작업전 pull 하여 변경된 사항을 가져오게함

- 깃헙 > settings > general > pull prequests
  Automatically delete head branches 체크, pr승인후 master브랜치에 머지되면 브랜치 자동삭제

- 깃헙 > settings > branches > branch protection rule(브랜치보호규칙적용) 
  Require a pull request before merging, master에 머지하기전 PR 필요
  Require approvals, PR 승인 필요

---

## git graph, vscode 익스텐션

- vscode 하단 왼쪽 상태바 git graph클릭하여 커밋 히스토리보기
- 커밋히스토리 마우스오른쪽으로 깃명령 사용가능

---

## git 협업을 고려한 작업방식

- 작업시작시 git pull origin master, 원격저장소 주브랜치 내용 가져와 로컬저장소에 동기화(원격에 변경사항이 있을수 있으므로)
- git switch -c feature/main-ui, 새로운 작업시 기능관련 브랜치 생성, 이동한 후 작업

## 작업완료후 커밋시작시

- 깃헙에 이슈추가(커스텀이슈템플릿 사용)
- git add . 작업완료후 변경사항 스테이지 추가
- git commit 로컬저장소에 이슈번호붙여서 커밋
- git push origin feature/main-ui, 원격저장소에 push
- PR(pull request템플릿 사용) 생성후 내용에 resolve: #이슈번호 넣으면 머지된후 해당이슈 자동으로 close됨
- git switch master로 이동후 git branch -D 브랜치명, 작업완료된 브랜치 삭제

---

## git 기본 명령어

- git add . 또는 파일명, 스테이지에 추가

- git restore --staged . 또는 파일명, unstage(vscode 소스제어 > 스테이징된 변경사항 -클릭)

- git status 작업디렉토리 변경내용, 수정사항 확인

- git diff 변경코드확인

- git branch 브랜치명, 브랜치만들기

- git switch 브랜치명, 브랜치이동

- git switch -c feature/main-ui 브랜치만들고 이동

- git branch 로컬브랜치확인

- git branch -a 로컬, 원격브랜치확인

- 로컬브랜치삭제: git switch master로 이동후 git branch -D 브랜치명

- 원격브랜치삭제: git push origin -d feature/main-ui

- git revert HEAD(해당브랜치 마지막 커밋) 원격에 올린 잘못된커밋을 이력남기고 되돌리기

## 기타

- vscode 터미널에서 프롬프트로 나가기 안될경우(터미널에 내용이 다 안보일경우 가끔나타남) q
