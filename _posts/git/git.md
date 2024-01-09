---
title:  "Git/Github"
category: git
typora-root-url: ../
toc: true
toc_sticky: true
---



## <br>Git

- 형상 관리 도구(Configuration Management Tool) 
- 다른말로 버전관리 시스템
- 프로젝트 소스 코드를 효과적으로 관리할 수 있는 시스템
  - 여러명이 동시에 작업하더라도 문제 X
  - 소프트웨어의 여러 버전을 동시에 관리 가능
  - 프로젝트 진행의 모든 로그를 볼 수 있으며 해당 시점으로 되돌리는 것도 가능

### <br>사용자 설정

- 로컬에서 사용할 Git 사용자 이메일과 이름을 설정
- git config Git에 관한 설정을 추가/변경/삭제하는 명령어
- 설정파일 종류
  - System 설정파일: 모든 시스템 사용자에게 적용(git config --system)
  - Global 설정파일: 한 사용자의 전치 Git Repository에 적용(git config --global)
  - Local 설정파일: 하나의 Repository에만 적용(git config --local)

```
Global Git 사용자 설정
git config --global user.email "abc@abc.com"
git config --global user.name "Hong gil-dong"

설정 확인
git config --list
```

- Github 계정에 ssh key 등록하기
  1. ssh key 만들기
     - [https://bit.ly/368zxvR](https://bit.ly/368zxvR)
  2. Github 접속 후 오른쪽 상단 프로필 클릭 Setting -> SSH and GPg Keys
  3. new SSH Key 클릭 후 Title과 복사한 Key 입력 후 Add SSH Key 클릭

### <br>초기화 및 삭제

- 명령어 : git init
- 초기화 할 대상 폴더에서 명령어 입력
- Git 초기화 시 폴더 안에숨김 폴더로 .git 폴더 생성(local Config 등으로 구성)
- .git 삭제시 git 삭제

### <br>.gitignore

- 사용자가 git에 등록(커밋)되지 않길 원하는 파일 또는 폴더들의 목록을 저장
- 작성법
  - #은 주석의 역할
  - 폴더: /폴더명(/docs)
  - 파일: 파일명.확장자(filename.txt)
  - 폴더 안 특정 확장자 파일 전부(/docs/*.txt)
  - 폴더 하위 모든 특정 확장자 파일 전부(/docs/\*\*/\*.txt)
- .gitignore 작성에 유용한 사이트
  - [https://gitignore.io](https://gitignore.io)

### <br>기본 동작 원리

- Working Directory: 작업하는 파일이 있는 디렉토리
- Staging Area: Git에 등록(커밋)할 파일들이 올라가는 영역
- Local Repository: **로컬** Git 프로젝트의 메타데이터와 데이터 정보가 저장되는 영역
- Remote Repository: Github 등의 서비스를 통한 **온라인** 상의 저장소

<img src="/../images/git/git.jpg" alt="git" style="zoom:80%;" />

### <br>기본 용어

- Origin: 원격 (Github 등의 온라인 저장소)에 있는 코드 
- Head: 내가 지금 작업하고 있는 로컬 브랜치 
- Add : Working Directory에서 Staging Area로 등록
- Commit : Staging Area에 등록된 파일을 Local Storage로 등록
- Commit Message : commit 시 함께 작성해 저장하는 메시지 (메모)
- Push : Local Storage에서 변경된 파일들을 Remote Repository로 등록
- Fetch : Remote Repository의 변경된 파일들을 Local Repository로 전달
- Merge : Local Repository의 변경사항을 Working Directory로 전달
- Branch : 독립적으로 어떤 작업을 따로 진행하기위한 가지
- Checkout : 사용할 다른 브랜치를 지정

### <br>Local Repository

- Repository: 파일이나 폴더를 저장하는 곳, Git 저장소는 파일 변경 이력별로 구분되어 저장
- Snapshot: 파일이나 폴더의 상태를 저장
- 내 PC에 파일이 저장되는 개인 저장 공간
- Local Repository 생성(원격 저장소에서 복사해 생성할 수도 있음)
  1. 원하는 폴더 생성
  2. 해당 폴더에서 git init 명령어 입력
  3. .git 폴더 생성 확인

### <br>Remote Repository

- 파일이 전용 서버(Github)에서 관리되며 여러사람이 함께 공유
- Github를 통해 생성
