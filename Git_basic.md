# Git Basic

---

> Git은 분산형 버전관리 시스템이다. 
>
> 소스코드의 이력을 확인하고, 협업 단계에서 활용할 수 있다. 

## 1. 기본 설정

---

* 윈도우에서 Git을 활용하기 위해서는 `git bash`가 필요하다.

  * [Git for Windows](https://gitforwindows.org/)

* 기본적으로 소스코드의 버전 정보를 기록하는 작성자(`author`) 설정이 필요하다.

  ```bash
  $ git config --global user.name "CN.Son"
  $ git config --global user.email "thschsmd@naver.com"
  ```

* 설정한 작성자 정보를 확인하기 위해서 아래 명령어를 실행한다. 

  ```bash
  $ git config --global -l
  user.email=thschsmd@naver.com
  user.name=ChoneungSon
  ```

### gitignore

> 프로젝트를 진행할 때, 개발 환경 혹은 프로젝트 사정상 Git으로 관리될 필요가 없거나, 올라가면 안되는 파일이 있다. 이러한 파일들을 `.gitignore`에 입력한다.

* 프로젝트 루트 경로에 위치시키는 것이 기본이지만, 하위 경로에 위치시켜도 하위 경로 기준으로 gitiignore 설정이 적용된다.

* 프로젝트를 시작할 때, 어떠한 내용을 적어야 할 지 모를 경우 [gitignore.io](https://www.gitignore.io/)에서 확인한다.

  ![image-20200121093657169](images/image-20200121093657169.png)

## 2. 로컬 저장소 활용법

---

### 2.1 Git 저장소 설정

특정 프로젝트 폴더에서 `git`을 활용하기 위해서 아래 명령어를 실행한다.

```bash
$ git init
Initialized empty Git repository in C:/Users/multicampus/Desktop/손초능/test/.git/
```

* `git init`이 정상적으로 완료되면, 루트 경로에 `.git`이라는 숨김 폴더가 생성된다. 앞으로 모든 git 관련 동작들은 이 폴더에 기록된다.

* git bash에서 `(master)`라는 브랜치 정보가 표기된다.

  ```bash
  multicampus@DESKTOP-KVCQHCD MINGW64 ~/Desktop/손초능/test (master)
  ```

### 2.2 add

>  `git`에서 `commit`을 하고 싶은 파일을 `staging area`로 이동시키는 명령어다.

``` bash
$ git add a.txt		# 특정 파일을 add -> stage
$ git add images/	# 특정 파일을 add -> stage
$ git add .			# 모든 파일 및 폴더를 add -> stage
```

### add 이전 상태

추적하고 있지 않은 파일이 있다고 말해주고 있으며, 친절하게 `git add` 명령어를 작성해보라고 권유하기까지 한다.

``` bash
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        a.txt
        b.txt

nothing added to commit but untracked files present (use "git add" to track)
```

### ad 이후 상태

add를 한 파일은 초록색 색상으로 commit 할 준비가 되었다고 말해주고 있고, add를 하지 않은 파일은 여전히 빨간 색상으로 추적하지 않는 파일이라고 말해준다.

``` bash
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt
```

따라서 git 작업을 할 때, 항상 `git status`명령어를 통해서 현재 상태를 확인해야 한다.



### 3. Commit

---

> 실제 Git을 통해 이력(버전)을 남기기 위해서는 `커밋(commit)`을 해야한다. 

* 커밋을 남길 때는 항상 커밋 메시지를 작성한다. 메시지는 해당 이력에 대한 정보를 가지고 있다.

  ```bash
  $ git commit -m "적절한 커밋 메시지 작성"
  [master (root-commit) 4eae761] 적절한 커밋 메시지 작성
   2 files changed, 0 insertions(+), 0 deletions(-)
   create mode 100644 a.txt
   create mode 100644 b.txt
  ```

* 커밋 이력을 확인하기 위해서는 아래 명령어를 실행한다.

  ```bash
  $ git log
  commit 4eae761cd04490fbb9945a55b07011ce95c16036 (HEAD -> master)
  Author: ChoneungSon <thschsmd@naver.com>
  Date:   Tue Jan 21 09:49:15 2020 +0900
  
      적절한 커밋 메시지 작성
  ```

* 이후 변경 사항이 발생하면 `add`->`commit`을 진행한다.

  * `add`: 커밋할 대상 파일을 선정하는 작업
  * `commit`: 이력을 확정하는 작업



## 4. 원격 저장소(Retome Repository) 활용하기

---

> Git != Github
>
> Git을 기반으로 원격 저장소를 제공해주는 서비스는 다양하다.
>
> 우리는 가장 범용적인 서비스인 Github을 기준으로 활용해보자.

### 4.1 기본 설정

#### 1) 원격 저장소 설정

원격 저장소(remote)를 origin이라는 이름으로 `github_URL`을 설정한다.

```bash
$ git remote add origin github_URL
```

* origin 말고 원하는 이름을 설정해도 되지만, 일반적으로 origin을 사용한다.

아래 명령어를 통해 저장된 원격 저장소 목록을 확인할 수 있다.

```bash
$ git remote -v
origin github_URL (fetch)
origin github_URL (push)
```

잘못 설정한 경우, 아래 명령어를 통해 삭제 가능하다.

```bash
$ git remote rm origin
$ git remote -v
```



## 4.2 Push

---

> 원격 저장소에 업로드 하기 위해서 `push`명령어를 사용한다.

`origin`으로 설정된 원격 저장소에 `push`한다. (== 업로드한다.)

``` bash
$ git push origin master
```

작업하기 전에 `git pull`, 작업 끝나면 `git push`를 잊지 않도록 하자. :)