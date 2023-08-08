# Git/GitHub

---

## 단어의 의미

Git : Version Control Systems. 단순히 버전을 관리해주는 소프트웨어

GitHub : 분산 버전 컨트롤 소프트웨어 깃을 기반으로 소스 코드를 호스팅 하고, 협업 지원 기능들을 지원하는 마이크로소프트의 웹서비스. 즉, _드라이브_ 같은 **원격 저장소**

repository : 커밋이 완료된 파일들의 **저장소**

commit : 특정 단위의 작업이 완결된 상태. 즉, **버전**

stage area : add 명령어에 의한 파일들이 commit 대기 상태에 있는 공간.

fast-forward : merge 할 때 현재 branch가 merge 하려는 branch보다 뒤쳐졌을 때 발생.
현재 branch의 버전이 merge하려는 branch의 commit을 가리키며, commit을 생성하지 않음.

recursive strategy : 현재 branch에 변경사항이 적용되어 merge하려는 branch와 다를 때 발생.
공통 조상을 이용하여 두 branch를 합치고 별도의 commit을 만듬.

HEAD : 가장 최근 커밋을 가리킴.

branch 충돌 : 같은 부분을 수정 후 merge하면 conflict 발생. 사용자가 직접 처리 또는 merge.tool 사용.

<img src="https://git-scm.com/book/en/v2/images/basic-branching-1.png" width=650px>

**master** branch는 현재 commit을 3번 한 상태(C0, C1, C2)

<img src="https://git-scm.com/book/en/v2/images/basic-branching-2.png" width=650px>

*iss53*이 발생하여 **iss53** branch를 C2 commit에서 생성함

<img src="https://git-scm.com/book/en/v2/images/basic-branching-3.png" width=650px>

_iss53_ 해결중 현재 서비스중인 **master** 에서 bug가 발생하여 일단 commit함(C3)

<img src="https://git-scm.com/book/en/v2/images/basic-branching-4.png" width=650px>

**hotfix** branch를 만들고 해결 후 commit함(C4) 이후 **master** 를 **hotfix** 로 merge 할 때 "fast-forward" 발생.

<img src="https://git-scm.com/book/en/v2/images/basic-branching-5.png" width=650px>

즉, commit message 없이 **hotfix**가 **master**에 포함됨.

<img src="https://git-scm.com/book/en/v2/images/basic-branching-6.png" width=650px>

기존에 작업중이던 **iss53** 에서 _iss53_ 해결 후 commit(C5).

<img src="https://git-scm.com/book/en/v2/images/basic-merging-1.png" width=650px>

현재 **master**(C4)는 _hotfix_ 적용되었지만 **iss53** 은 적용되지 않았기에 "recursive strategy" 발생.

<img src="https://git-scm.com/book/en/v2/images/basic-merging-2.png" width = 650px>

공통 조상(C2) commit을 이용하여 3-way Merge 실행.
즉, **master** 에 'C4와 C5를 부모로 가진다'는 내용의 commit(C6)이 자동으로 생성됨.

---

## Git 명령어

- git config --global user.name : commit에 같이 저장 될 사람(나)의 이름 지정

  ```git
  git config --global user.name "SungChul CHA"
  ```

- git config --global user.email : commit 같이 저장 될 사람(나)의 메일 주소 지정

  ```git
  git config --global user.email "sungchulcha13@gmail.com"
  ```

- `git config --list` : 위에서 지정한 정보들 확인
  <br>
- `git init` : 디렉토리를 깃 리포지토리로 초기화 시키는 명령어
  <br>
- git add : 버전 관리를 위해 파일을 추가하는 행위

  - 현재 경로의 모든 파일을 추가할 때.

  ```git
  git add .
  ```

  - 특정 파일을 지정할 수도 있다.

  ```git
  git add f1.txt
  ```

- git commit : add로 추가한 파일의 버전을 지정.

  - commit message까지 작성하는 명령어

  ```git
  git commit -m "first commit"
  ```

  - 한 번 add 했던 파일들은 `-am` 명령어로 add와 commit 한번에 가능

  ```git
  git commit -am "commit message"
  ```

- `git status` : 현재 git의 상태를 확인하는 명령어. add 안된 파일 혹은 commit 안된 파일을 알 수 있다.
  <br>

- `git log` : 버전의 변경 이력들을 출력

  ```git
  commit 700afaa0b9c2c4d9ff9869341f55c7037bf44f81 (HEAD -> master)
  Author: SungchulCha <tony4907813@gmail.com>
  Date:   Tue Aug 8 23:19:38 2023 +0900

    git log 예시를 위해 commit 함

  commit ebee42094bd370662d9752e060cba14a64846b3e (origin/master)
  Author: SungchulCha <tony4907813@gmail.com>
  Date:   Tue Aug 8 22:35:34 2023 +0900

    내용 작성 완료. ToDo: 내용 순서들 정리.
  ```

- `git log --branches --decorate` : branch 포함한 변경 이력 보여줌
  `git log --branches --decorate --grpah --oneline`
  `git log --branches --decorate --graph`

  ```git
  * commit f69039b61febadb8a0592f4d9869027b9d22815a (HEAD -> master, origin/master)
  | Author: SungchulCha <tony4907813@gmail.com>
  | Date:   Tue Aug 8 23:23:03 2023 +0900
  |
  |     git log --branches 예시용 commig.
  |
  * commit 700afaa0b9c2c4d9ff9869341f55c7037bf44f81
  | Author: SungchulCha <tony4907813@gmail.com>
  | Date:   Tue Aug 8 23:19:38 2023 +0900
  |
  |     git log 예시를 위해 commit 함
  |
  * commit ebee42094bd370662d9752e060cba14a64846b3e
    Author: SungchulCha <tony4907813@gmail.com>
    Date:   Tue Aug 8 22:35:34 2023 +0900

      내용 작성 완료. ToDo: 내용 순서들 정리.
  ```

- `git log -p` : 커밋 사이의 변경점 확인 가능

  ````
  commit f69039b61febadb8a0592f4d9869027b9d22815a (HEAD -> master, origin/master)
  Author: SungchulCha <tony4907813@gmail.com>
  Date:   Tue Aug 8 23:23:03 2023 +0900

    git log --branches 예시용 commig.

  diff --git a/README.md b/README.md
  index 5669938..02b73c2 100644
  --- a/README.md
  +++ b/README.md
  @@ -91,8 +91,28 @@ _iss53_ 해결중 현재 서비스중인 **master** 에서 bug가 발생하여
   git commit -am "commit message"
    ```

  -git log : 버전의 변경 이력들을 출력
  -git log --branches --decorate : branch 포함한 변경 이력 보여줌
  +- `git log` : 버전의 변경 이력들을 출력
  +
  +  ```git
  +  commit 700afaa0b9c2c4d9ff9869341f55c7037bf44f81 (HEAD -> master)
  +  Author: SungchulCha <tony4907813@gmail.com>
  +  Date:   Tue Aug 8 23:19:38 2023 +0900
  ````

  > git log에서 commit 옆에 있는 문자열은 해당 commit의 id

- git diff id..id : 특정 commit 사이의 차이점 보여줌

  ```
  git diff f69039b61febadb8a0592f4d9869027b9d22815a..ebee42094bd370662d9752e060cba14a64846b3e
  diff --git a/README.md b/README.md
  index 02b73c2..75719ca 100644
  --- a/README.md
  +++ b/README.md
  @@ -1,118 +1,27 @@
  -# Git/GitHub
  +<h1>Git/GitHub</h1>

  ----
  -
  -## 단어의 의미
  -
  -Git : Version Control Systems. 단순히 버전을 관리해주는 소프트웨어
  -
  -GitHub : 분산 버전 컨트롤 소프트웨어 깃을 기반으로 소스 코드를 호스팅 하고, 협
  업 지원 기능들을 지원하는 마이크로소프트의 웹서비스. 즉, _드라이브_ 같은 **원격 저장소**
  -
  -repository : 커밋이 완료된 파일들의 **저장소**
  -
  -commit : 특정 단위의 작업이 완결된 상태. 즉, **버전**
  -
  -stage area : add 명령어에 의한 파일들이 commit 대기 상태에 있는 공간.

  ```

git log master..name : branch 사이의 차이를 보여줌
git diff master..name : branch 사이의 현재 차이점을 보여줌

git reset ID --hard : 해당 commit으로 돌아감. (복구 가능) !원격 저장소에서 reset은 절대 하면 안됨!
--hard : 강제적으로 리셋

git revert : 해당 commit으로 새로운 버전을 만들어냄

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

## Git과 GitHub 사용 과정

**(팀장)**

> git init
> git add .
> git commit -m "commit message"
> git remote add origin https://github.com/SungChul-CHA/git.git
> git push -u origin main

_(사원)_

> git clone https://github.com/SungChul-CHA/git.git Floder_Name
> git checkout -b Branch_Name
> (작업)
> git add .
> git commit -m "commit message"
> git push origin Branch_Name
> (깃헙에서)PR 작성

**(팀장)**

> (깃헙에서)PR 확인 후 merge
> 충돌시 <a href="#단어의-의미">merge conflict 확인</a>
> git add .
> git commit -m "commit message"
> git pull
> 충돌시 <a href="#단어의-의미">merge conflict 확인</a>
> (작업)
> git push

---

**커밋은 되도록 하나의 작업이 완료되면 작성**

**pull, push 항상 합시다!**
[![조코딩 Youtube](http://img.youtube.com/vi/h2MqgqDMvLI/0.jpg)](https://www.youtube.com/shorts/h2MqgqDMvLI)

sourcetree

---
