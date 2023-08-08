<h1>Git/GitHub</h1>

<h2>Git이란</h2>
Git : Version Control Systems

## Git 명령어

git init : 디렉토리를 깃 리포지토리로 초기화 시키는 명령어

git add : 버전 관리를 위해 파일을 추가하는 행위
현재 경로의 모든 파일을 추가할 때 `git add .`
특정 파일을 지정할 수도 있다. `git add f1.txt`

git commit : add로 추가한 파일의 버전을 지정.
git commit -m : commit message까지 작성하는 명령어

git commit -am "message" : 한 번 add 했던 파일들은 -am명령어로 add와 commit 한번에 가능

```
git commit -m "message"
```

git log : 버전의 변경 이력들을 출력
git log --branches --decorate : branch 포함한 변경 이력 보여줌
git log --branches --decorate --graph
git log --branches --decorate --grpah --oneline

git log -p : 커밋 사이의 변경점 확인 가능

git log에서 commit 옆에 있는 문자열은 해당 commit의 아이디

git diff : 특정 commit 사이의 차이점 보여줌

```
git diff ~~~..~~~
```

git log master..name : branch 사이의 차이를 보여줌
git diff master..name : branch 사이의 현재 차이점을 보여줌

git status : 현재 git의 상태를 확인하는 명령어
add 안된 파일 혹은 commit 안된 파일을 알 수 있다.

git reset ID --hard : 해당 commit으로 돌아감. (복구 가능) !원격 저장소에서 reset은 절대 하면 안됨!
--hard : 강제적으로 리셋

git revert : 해당 commit으로 새로운 버전을 만들어냄

git config --global user.name : commit 한 이(나)의 이름 지정

git config --global user.email : commit 한 이(나)의 메일 주소 지정

git config --list : 위에서 지정한 정보들 확인

git config --global core.autocrlf true : \r\n 설정 편하게 하는거.

git branch : branch들을 보여줌

git branch name : name이란 이름의 branch가 만들어짐

!master(병합할 branch에서 명령어 작성)
git merge name : name의 commit들을 현재 branch로 병합

git branch -d name : name branch를 삭제함

git branch -b name : name이란 branch를 만들고 해당 branch로 checkout함

git checkout name : 기존의 branch에서 나가서 name 이란 branch로 이동함
checkout 할 때 commit을 하지 않으면 해당 branch에서 변경된 작업들이 checkout하려는 branch까지 영향을 끼치는 문제가 발생함.

git stash : 버전관리되고 있는 파일들의 작업 상황을 다른 공간에 숨겨줌.

git stash apply : 가장 최근에 숨겨놨던 작업을 다시 적용시켜줌.

git stash drop : stash에 있던 작업 하나 삭제.

git stash pop : apply 하고 drop 함.

git stash list : 숨겨놨던 작업들의 list를 보여줌
직접 삭제하지 않는이상(reset명령어로는) 삭제 안됨.

git init --bare : 작업 불가능한 repository 생성

git remote add origin 저장소경로 : 원격 저장소를 현재 디렉토리에 연결. 저장소 경로를 origin이란 단어로 대체. 다른 단어도 됨.

git remote -v : 원격 저장소 보여줌

git remote remove origin : 원격 저장소 연결 삭제

git push : remote repository로 commit을 동기화함.(업로드)

git push -u origin master : local repository의 master branch를 origin repository의 master branch로 push하겠다.(한번만 하면 됨)

git clone 주소 . : 현재 directory를 git repository로 설정하고 주소의 원격 저장소랑 연결한다.(git init 굳이 먼저 안해도됨)

git pull : 연결된 원격 저장소의 파일들을 다 가져옴.

git fetch : remote repository의 commit(verison)이 local repository의 commit과 다를 때 local repository의 master branch가 강제적으로 remote repository의 origin branch로 이동하지 않아서 변경 사항을 확인 가능함.
-> git fetch + git merge = git pull

git tag 1.0.0 master : 1.0.0이라는 이름의 tag를 만들어서 master branch가 가리키는 commit을 가리킴.
tag는 commit을 해도 branch와 다르게 바뀌지 않음.
git checkout 1.0.0 도 가능

git tag -a 1.1.0 -m "message" : tag에 message 작성

git push --tags : tag도 realese로 업로드 됨.
깃헙에서 직접 tag에 대한 설명 작성 가능

git tag -d 1.1.0 : 1.1.0 tag 삭제

---

stage area : add 명령어로 파일들이 commit 대기 상태에 있는 공간
리포지토리 : 커밋이 완료된 파일들의 저장소
버전 : 특정 단위의 작업이 완결된 상태

---

커밋은 되도록 하나의 작업이 완료되었을 때 작성

sourcetree

fast-forward : merge 할 때 현재 branch가 merge 하려는 branch보다 뒤쳐졌을 때
현재 branch의 버전이 merge하려는 branch의 version(commit)을 가리키며, commit을 생성하지 않음.
recursive strategy : 현재 branch에 변경사항이 적용되어 merge하려는 branch와 다를 때
공통 조상을 이용하여 두 branch를 합치고 별도의 commit을 만듬

HEAD : 가장 최근 커밋을 가리킴

branch 충돌 : 같은 부분을 수정 후 merge하면 conflict 발생. 사용자가 직접 처리 또는 merge.tool 사용

git init
git add .
git commit -m "message"
git remote add origin 깃헙주소
git push -u origin main

git clone 깃헙주소 폴더이름
git checkout -b 브랜치이름
작업
git add .
git commit -m "커밋메세지"
git push origin 브랜치이름
(깃헙에서)PR 작성

(깃헙에서)PR 확인 후 merge
git add .
git commit -m "commit message"
git pull
충돌시 merge conflict 확인
작업
git push
