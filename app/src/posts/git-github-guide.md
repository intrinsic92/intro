# git, github 완벽 정리

git과 github의 대한 명령어 정리

## git

### git 설치
https://git-scm.com/install/ 경로로 들어가서 본인에 맞는 설치 파일 받은 후 설치
설치가 완료 되면 명령어 창에서 명령어로 확인 가능
```bash
git -v
git --version

result
git version 2.50.1.windows.1
```

### git 프로젝트 경로 설정 및 지정
본인이 원하는 프로젝트 경로를 이동 후 깃으로 연결할 폴더를 지정한다.
```bash
cd #내 프로잭트 경로#
git init
```
이렇게 하면 해당 폴더에 .git 파일이 생성 되고
```bash
git status
```
로 정상적으로 init이 됐는지 확인 가능

### git 상태 확인 명령어
```bash
##현재 상태 
git status
##현재 로컬 커밋된 특정 파일만 한번에 비교
git diff app\src\posts\git-github-guide.md --no-pager
#스테이징에 있는 파일과 비교
git diff app\src\posts\git-github-guide.md --staged --no-pager
```

### git 로컬 브랜치 확인 방법
```bash
#브랜치 목록 확인
git branch
```
로 현재 브랜치를 확인 할 수 있고 branch는 기본 main으로 잡히고 생성된다.

### git 로컬 브랜치 생성 및 변경 방법
기본적으로는 하나의 로컬 브랜치만 사용하면 문제 없으나 버전 관리를 위해 처리를 하기 위해서는 브랜치를 변경해야한다. 
이때 사용하는 생성 명령어 및 변경 명령어는 다음과 같다.
```bash
#브랜치 생성
git branch 브랜치명
#Git 2.23 이전 버전 브랜치 변경 및 생성 후 변경 명령어
git checkout 브랜치명
git checkout -b <새로운_브랜치명>
#git 2.23 이후 버전 브랜치 변경 및 생성 후 변경 명령어
git switch <브랜치명>
git switch -c <새로운_브랜치명>
```

### git 로컬 스토리지 commit 방법 및 제어
```bash
#모든 변경된 파일 스테이징 등록
git add . 
#특정 변경된 파일 스테이징 등록
git add #상대경로#
#commit 명령어
git commit -m "커밋내용"

#커밋된 상태로 되돌리기
git restore <file>
#스테이징 영역에서 제거 최신 깃에서 권장방식
git restore --staged <file>
#스테이징 취소 위와 내용은 동일
git reset <file>

#커밋 상태 완전 초기화 하고 마지막 커밋 상태로 돌림
git reset --hard HEAD
#커밋 상태를 이전 commit의 해더로 위치 시키고 스테이징 디렉토리를 유지 시킴
git reset --soft HEAD~1
```

### git 임시저장소 활용을 위한 명령어
임시저장소는 git에서 커밋을 하지 않았으나 로컬에 기록을 하고 싶은 경우나 다른 작업으로 커밋할정도는 아니나 기록을 남기는 경우 아니면 충돌이 난 경우에 대한 원본 저장을 위해 활용하거나 하는 임시저장하는 명령어이다.
```bash
#현재 수정된 파일 임시저장소에 저장하는 명령어
git stash
#현재 스테이징된 파일 유지
git stash --keep-index
#현재 모든 파일 유지
git stash --keep-worktree
#특정 파일만 임시저장소에 저장하는 명령어
git stash push path/to/file1 path/to/file2
#신규 저장된 파일도 같이 임시저장소에 저장하는 명령어
git stash -u
혹은
git stash --include-untracked
#현재 임시저장소에 저장된 리스트를 보여주는 명령어
git stash list
#가장 최근 스태시(stash@{0})나 지정된 스태시의 변경 사항을 현재 브랜치에 적용 명령어
git stash apply "stash@{N}"
#가장 최근 스태시로 적용하고 기존 스태시 삭제하는 명령어
git stash pop "stash@{N}"
#스태시 영구삭제 명령어
git stash drop "stash@{N}"
#모든 스태지 날리는 명령어
git stash clear
#새로은 브랜치에 스태지에 저장된 내용 따서 등록하는 명령어
git stash branch <new-branch-name>
```

## github
### 깃허브 계정 연동 명령어
```bash
#브랜치 목록 확인 글로벌 설정으로 이름 이메일 등록
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```
### github 계정 연동 설정 확인
```bash
git config --global --list
혹은
git config --global user.name
git config --global user.email
```

### github 원격저장소 붙이기
```bash
origin은 기본 원격 저장소 명칭
git remote add origin https://github.com/내계정/저장소.git

만약 원격저장소를 변경하고 싶다면
git remote remove origin로 삭제 후 다시 등록
git remote add origin https://github.com/내계정/저장소.git
그냥 변경하고 싶다면
git remote set-url origin https://github.com/내계정/새저장소.git
```
### 내 로컬 브랜치 및 원격 브랜치 확인
```bash
#내 로컬 브랜치 및 원격 브랜치 확인 명령어
git branch -vv
#원격 브랜치만 확인 명령어
git branch -r
#현재 원격저장소 어디에 붙어 있는지 확인 명령어
git remote -v
(fetch)는 가지고오는 경로
(push)는 보내는 경로
```

### 최초 원격 브랜치 푸쉬
```bash
#origin 원격 저장소 이름이고 main원격 브랜치 명이고 최초 푸쉬시에는 -u로 지정해줘야 이후 부시할 때는 같은데로 푸쉬함
git push -u origin main
```

### 원격 브랜치 최신정보 가지고 오기 및 파일 가지고오기
```bash
#origin 원격 저장소 이름이고 main원격 브랜치 명이고 최초 푸쉬시에는 -u로 지정해줘야 이후 부시할 때는 같은데로 푸쉬함
# 패치 명령어로 현재 원격레파지토리의 최신 정보를 가지고 옴
git fetch origin
# 현재 원격래파지토리정보 가지고 온 후 원격브랜치 -> 로컬 브랜치로 최종 push 내용 가지고 옴
git pull origin main
```

### pull의 세부 정보
```bash
#두개의 명령어를 포함한게 pull이다
# 1. 원격의 최신 내용을 가져옵니다. (파일에 영향 없음)
git fetch origin
# 2. 원격 브랜치를 현재 로컬 브랜치에 병합 시도합니다.
git merge origin/<브랜치명>
```




