# Git

-   프로그래밍을 하다가 어느 지점에서 처음 저장하는 지점을 `세이브포인트1` 이라고 하자.  
    저장을 한 뒤, 프로그래밍을 하다가 `세이브포인트2`에 다시 저장을 하고 또 작업을 하다보니,
-   _다양한 이유 혹은 에러들로 이전으로 돌아가야 하는 경우\*_가 있다.  
    이러한 경우에 **이전 버전을 다시 가져올 수 있다.**
-   **버전 제어**와 **협업**에 필수적이다.

---

```
$ mkdir Story                // Story라는 폴더를 만들었다.
$ cd Story                   // Story 폴더로 이동했다.
$ touch chapter1.txt         // Story 폴더 안에 chapter1.txt 라는 파일을 만들었다.
$ open chapter1.txt          // chapter1.txt 파일을 열어서 hello world!라는 간단한 내용을
                                                         // 적고 저장했다.
```

-   Story라는 폴더에 `chapter1.txt`라는 파일을 만들고 안에 간단한 `hello world!` 라는 내용을 넣고 저장했다.

---

```
$ git init                    // git을 생성한다.
$ ls -a                       // 파일리스트를 보면 .git이라는 숨긴 파일이 있는 것을 볼 수 있다.
                              // .git을 통해 모든 변경 사항을 추적하고  
                              // 변경사항을 커밋하고 버전제어를 한다.
```

-   지금 있는 이 위치를 **워킹 디렉토리**라고 할 수 있는데, 우리는 `chapter1.txt` 라는 파일을 **스테이징 영역**으로 추가해야한다.
-   **스테이징 영역**은 파일을 선택하고 커밋할 수 있는 디렉토리이다.

---

```
$ git status                  // 현재 스테이징 영역에 무엇이 있는지 확인할 수 있다.
```

-   `git status` 를 입력하면 `chapter1.txt`가 **빨간 글씨**로 나오면서 아직 **스테이징 영역**으로 이동되지 않은 것을 확인 할 수 있다.

---

```
$ git add chapter1.txt        // chapter1.txt를 스테이징 영역에 추가한다.
```

-   이후 다시 `git status` 를 입력하면 `chapter1.txt` 가 **스테이징 영역**에 추가된 것을 확인할 수 있다.

---

```
$ git commit -m "Complete Chapter 1"
// "Complete Chapter 1" 이라는 메시지와 함께 스테이징 영역에 있는 파일을 commit 한다.
```

-   메시지를 명확하게 남기는 것이 중요하다. 나중이나 다른 사람이 봤을 때 어떤 작업을 했는 지를 알 수 있기 때문이다.
-   completed와 같은 과제 시제가 아닌 현재 시제를 쓰는 것이 룰이라고 한다.

---

```
$ git log          // 어떤 commit을 수행했는지 누구에 의해 몇시에 commit된 것인지 알 수 있다.
                   // 또한 어떠한 메시지를 남겼는지도 알 수 있다.
```

---

```
$ touch chapter2.txt
$ touch chapter3.txt
// 2개의 Chapter 파일을 더 만들었다.

$ git add .           // git add . 라는 명령어로 현재 디렉토리에 있는 모든 파일들을
                      // 스테이징 영역에 추가할 수 있다.
$ git commit -m "Add Chapter2 & Chapter3"   // Chapter 2,3을 commit했다.
$ git log             // git log로 기록을 확인한다.
```

-   2개의 캡쳐 파일을 더 만들고 간단한 내용을 적은 뒤, add, commit을 했다.
-   `git log` 를 통해서 확인해보면 같은 사람이 약 6분전 chapter1을 올렸고, 방금 chapter2,3을 올렸다는 내용과 commit message도 함께 보여진다.
-   commit된 파일들은 이제 **로컬 레포지토리**에 있게 된다.

---

### 스테이징 영역

-   모든 파일을 추적하거나 추가하고 싶지 않을 수도 있다.
-   또한, git이 무시하기를 원하는 것이 무엇인지를 알아내기 위해 **스테이징 영역**이 존재한다.

---

### 롤백

-   `chapter3.txt` 작업을 하다가 잠들어서 이상한 문구를 막 친 상태로 저장을 했다고 생각해보자.

```
$ git diff chapter3.txt  // chapter3 commit 시점과 
                         // 현재 저장된 시점의 차이(difference)를 보여준다.

$ git checkout chapter3.txt    // chapter3이 commit 시점으로 되돌려준다.
```

-   아무리 이상한 내용을 치고 저장을 했어도 가장 마지막 commit 시점으로 되돌아갈 수 있다.

---

### Github

-   분산 버전 컨트롤 소프트웨어 깃(Git)을 기반으로 소스 코드를 호스팅 하고, 협업 지원 기능들을 지원하는 현재 가장 인기 있는 소스 코드 호스팅 서비스이자 소셜 코딩 플랫폼이다.
-   회원가입 후에 `New repository`를 이용해서 저장소를 만든다.
-   `Public`은 모든 사람이 나의 소스를 볼 수 있고, `Private`은 볼 수 없게 설정할 수 있다.  
    중요한 프로젝트가 아니라면 가능한 소스를 공유하자.
-   `Initialize this repository with a README` 는 체크하지 않고 만든다.  
    이는 이따가 설명할 것이다.

```
Story라는 repository를 만들었다.
https://github.com/jehyuksong/Story.git 과 같은 문구를 볼 수 있는데 이를 복사해둔다.
```

---

```
$ git log              // 현재 나의 로컬 레포지토리에는 2개의 커밋을 했던 내용이 뜬다.
                                             // 이 커밋된 내용들을 나의 깃허브 레포지토리에 푸시를 해주려고 한다.
```

```
$ git remote add origin https://github.com/jehyuksong/Story.git
// 만든 깃허브 저장소와 연동시키는 리모컨을 만든다.
```

-   이제 `origin` 이라는 복제된 원격 저장소가 생성되어서 푸시를 할 수 있다. 관례적으로 `origin` 이라는 이름을 사용한다.

---

```
$ git push -u origin master     // 로컬 저장소를 원격 저장소로 푸시한다.
// 혹여나 username for 'https //github.com' : 같은 내용이 뜬다면 github 유저 네임과 
// password for 'https //github.com': 패스워드를 작성하면 push가 완료된다.
```

-   `-u` 는 원격저장소와 로컬저장소를 연결하는 명령어이다.
-   `origin` 은 원격저장소 remote의 이름, `master` 는 branch의 이름인데, 기본 branch가 `master`이다.
-   결국 `origin` 이라는 원격 저장소의 `master branch` 를 push 하는 것이다.
-   Github로 가서 새로고침을 해보면 chapter1,2,3.txt가 commit message와 함께 올라와있는 것을 볼 수 있다.
-   깃허브에서 `commit` 을 확인해보면 몇 개의 세이브포인트가 있는지, 파일의 어떤 내용이 변경된건지 커밋 메시지는 무엇인지 등 모든 내용을 확인할 수 있다.

---

### master branch

-   `master branch` 는 commit 또는 세이브포인트의 주요 branch이며, 순차적이다.
-   일반적으로 주요 진행 상황이 저장되거나 commit되는 곳이다.
-   .git 으로 된 master branch를 push함으로써 github의 원격저장소에 저장하는 것이다.

---

### gitignore

-   특정 파일을 로컬 밋 원격 git repository에 commit 하는 것을 방지한다.

```
$ cd desktop                // desktop 디렉토리로 이동
$ mkdir project             // project 폴더를 생성
$ cd project                // project 폴더로 이동
$ touch file1.txt file2.txt file3.txt secrets.txt    // file1,2,3과 secrets파일 생성
```

-   `secrets.txt` 파일 안에는 **password, Api key**와 같은 공개되어서는 안되는 내용이나 용량이 큰 **modules**, 다른 사람들이 갖고 싶지 않은 **유틸리티 파일, 로컬 설정** 또는 **기본 설정**과 관련된 파일들이 있다고 가정해보자.
-   이를 github와 같은 개방형 플랫폼에 호스팅되는 것을 원하지 않는다.
-   작업을 함에 있어서 부분을 잘 생각하고 무엇을 넣을지 인식하는 것은 매우 중요하다.

```
$ touch .gitignore         // .gitignore 파일을 생성
$ ls -a                    // 숨겨진 파일이라 ls -a를 사용하면 만들어진 것을 볼 수 있다.
$ git init                 // git init을 한다.
$ git add .                // 모든 git을 추가한다.
                           // secrets.txt도 추가가 된다.
$ git rm --cached -r .     // 모든 항목이 git 스테이징 영역에서 제거한다.
```

-   `.gitignore`에 아무런 내용이 없기 때문에 모든 파일들이 추가되는 것을 볼 수 있다.

```
// 이제 .gitignore 파일을 열고 안에 secrets.txt를 추가한다.
```

-   `.gitignore` 는 규칙이 있는데 작성할 파일을 새로운 줄에 써야하고, `#` 을 이용해서 주석을 달 수 있다.
-   또한 모든 .txt 확장자 파일들을 전부 add 하고 싶지 않다면 `*.txt` 와 같이 별표를 이용해서 사용할 수 있다.

```
$ git add .             // git의 모든 내용을 add한다.
$ git status            // secrets.txt 파일을 제외한 나머지의 파일들만 올라간 것을 볼 수 있다.
```

### github/gitignore

-   github에 가서 `github/gitignore`를 검색해보면 언어별로 주요 작업들 별로 `.gitignore` 에 들어갈 내용들이 템플릿으로 만들어놓은 것이 있다. 이 내용들을 기본적으로 그대로 복사해서 붙여 넣고 더 추가하고 싶은 내용들을 추가해나가면 된다.

---

### git clone

-   원격 저장소를 복제하여 로컬 컴퓨터로 가져오는 방법이다.
-   특정 원격 저장소의 커밋 및 모든 버전을 확인하고 파일을 나의 워킹 디렉토리로 가져올 수 있다.

### 방법

-   github의 아무 소스에나 들어가서 `code` 버튼을 누르면 `Clone with HTTPS` 에 적혀있는 `URL`을 복사한다.

```
$ cd desktop                // desktop 디렉토리로 이동
$ git clone https://github.com/themaxsandelin/todo.git  // 복사한 URL을 복제한다.
```

-   desktop을 보면 `todo` 라는 폴더를 볼 수 있다. 방금 복제한 파일이다.
-   모든 프로젝트 파일과 소스코드들이 전부 담겨있다.

```
$ cd todo                 // clone한 디렉토리로 이동한다.
$ git status              // 상태를 확인한다.
```

-   commit된 내용들을 똑같이 확인할 수 있다.
-   git cloning은 스켈레톤 프로젝트를 가져올 때도 유용하게 사용될 수 있다.

---

### branch, branching

-   버전 1과 버전 2가 있다고 생각하고 간단한 예를 들어보자.
-   로컬 저장소에는 2개의 커밋이 생성되었을 것이다.
-   이제 우리는 다른 것을 시도해보고 새로운 기능을 구축하고 싶다는 생각을 하게 된다.  
    그러나 이 때 우리는 새로운 아이디어나 시도들로 엉망을 만들 위험이 있다.
-   그래서 우리는 메인 브랜치인 마스터 브랜치에 계속 커밋하는 것이 아니라 원하는 만큼 사이드 브랜치를 생성할 수 있다.
-   사이드 브랜치로 업데이트와 새로운 시도를 하는 동시에 우리는 메인 브랜치의 개발도 계속 할 수 있다.  
    마치 branch 단어 뜻대로 `가지를 쳐서 나아가는 것` 과 같다.
-   진행하다가 사이드 브랜치에서의 기능이 성공적이고 유용할 경우 메인 브랜치와 병합을 할 수 있다.
-   `새로운 기능을 개발`하거나 `버그를 수정`하는 것들이 메인 프로젝트를 망가뜨릴 수 있으므로 사이드 브랜치에서 진행을 하고 정상적으로 작동할 경우 마스터 브랜치로 다시 가져오는 것이다.
-   **브랜치를 많이 만들어도 메모리나 디스크 공간에 부담이 되지 않기 때문에 작업을 커다란 브랜치로 만들기 보다, 작은 단위로 잘게 나누느 것이 좋다.**

### 작동 방법

```
$ cd desktop/Story          // chapter1,2,3.txt 을 만들었던 디렉토리로 이동
$ git branch alien-plot     // alien-plot 이라는 branch를 만든다.
$ git branch                // branch를 확인한다.

```

-   branch를 확인하면 `master` 와 `alien-plot` 이라는 branch가 있는 것을 확인할 수 있다.  
    또한 `master` 앞에 `*` 가 되어있는데 이는 **현재 어떤 브랜치에 있는지**를 보여준다.

---

```
$ git checkout alien-plot       // alien-plot 브랜치로 이동
$ open chapter1.txt
$ open chapter2.txt             // chapter1과 chapter2를 열어서 내용을 수정한다.
$ git add .                     // 모든 파일을 add한다.
$ git commit m "alien theme"    // commit을 진행한다.
$ git log                       // git log를 확인한다.
```

-   `git log` 를 확인하면 `alien-plot` 이라는 브랜치에서 commit된 내용을 확인할 수 있다.

```
$ git checkout master           // master branch로 돌아간다.
$ open chapter1.txt
$ open chapter2.txt             // chapter1,2가 변경되지 않고 원래 그대로이다.
$ touch chapter4.txt            // chapter4.txt 를 만든다.
$ open chapter4.txt             // chapter4.txt를 열어서 아무 내용이나 적고 저장한다.
$ git add .
$ git commit -m "add chapter4"  // git add,commit한다.
```

### 병합

```
// master branch에 있는 상황

$ git merge alien-plot          // alien-plot과 병합한다.
                                                                // vim이 뜨면 기본상태로 :q! 하거나
                                // 메시지 수정 후 :wq! 를 하고 나오면 된다.
$ git log            // 가장 최근 commit에 alien-plot과 병합한 내용이 나온다.
                                         // chapter1,2의 내용도 alien-plot의 내용처럼 바뀌었다.
$ git push -u origin master      // git push를 진행한다.
```

-   `Github` 로 이동해서 저장소를 확인하면 commits이 여러개 추가되어 있을 것이다.
-   **alien-plot branch를 만들어 커밋**한 내용, **master에 chapter4를 추가**한 내용, **master에 alien-plot를 병합**한 것까지 추가되었다.
-   또한 `insights - network` 를 들어가면 그 과정을 그래프로 확인할 수도 있다.

---

### Github에서 branch 컨트롤하기

-   github로 가서 이번에는 `Story2` 라는 `Initialize this repository with a README` 가 체크된 repository를 생성한다.
-   `README` 파일은 어떤 프로젝트인지를 설명할 수 있는 곳이다.  
    나의 저장소를 보고있는 사람들에게 다양한 설명을 할 수 있고, 가장 먼저 보여진다.
-   `Story2` 라는 저장소에서 `Add file - Create new file`을 클릭해서 새로운 파일을 만든다.
-   `chapter1.txt` 라는 파일명으로 아무 내용이나 적고 아래 코멘트를 달고 올린다.
-   `branch` 에서 `experimental` 이라는 branch를 만들고 `chapter1.txt` 의 내용을 수정하고 저장한다.
-   이제 저장소 메인으로 돌아가면 `Compare & pull request` 라는 버튼이 생긴 것을 볼 수 있다.
-   이어서 바로 `master branch` 에 `chapter2.txt` 이라는 file을 생성한다.
-   이제 `experimental branch` 를 `master branch` 로 가져오고 싶다면 **현재 위치**가 `master branch` 인 상태로 `Compare & pull request` 버튼을 클릭한다.
-   **base** = `master` , **compare** = `experimental` 인 상태로 `create pull request` 버튼을 클릭해서 병합을 진행한다. 간단한 내용을 적은 뒤 `Confirm merge` 버튼을 통해 병합이 완료된다.
-   화면상으로 볼 수 있다는 장점이 있지만 `CLI` 로 진행하는 것이 더 간편하다는 것을 알 수 있다.

---

# Fork / 협업

-   `다른 사람의 Github repository`에서 **어떤 부분을 수정하거나 추가하고 싶을 때** 해당 저장소를 `나의 Github repository`로 **그대로 복제**하는 기능이다.
-   `fork한 repository`는 **원본과 연결**되어 있다.
-   **원본에 변경 내용을 적용**하고 싶으면 해당 `원본 repository에 pull request`를 한다.  
    그리고 **원본 관리자가 변경 사항을 검토하고 승인하면 병합되어서 원본에 반영**되는 것이다.  
    승인되기 전에는 나의 Github repository에 있는 fork된 repository 에만 변경된 것이 적용된다.
-   push의 권한이 없기 때문에 pull 요청을 하는 것이다.
-   **clone** 과 차이점을 구분해야 한다.
-   **협업**할 때 매우 유용하게 사용된다.

### 방법

-   **다른 깃허브 계정(B 계정)**으로 로그인한다.
-   **원본 계정(A 계정)**의 Story repository를 검색해서 찾는다.
-   `Fork` 버튼을 클릭해서 복제한다.
-   **B 계정**의 repository에 Story repository가 추가된다.
-   몇 가지 내용을 변경하고 commit한다.
-   **B 계정**의 repository에서만 변경되고 commit 기록을 보면 이 전의 기록에 이어서 **B 계정**에 의해서 commit이 되었다는 것과 함께 **B 계정**의 master branch가 변경된 것을 확인할 수 있다.
-   이제 다시 **A 계정**으로 로그인을 한다.
-   commit을 확인해보면 **B 계정**에 의해 변경된 별도의 지점으로 표시되지만 **A 계정**의 master branch에는 영향을 주지 않는다.
-   **A 계정**의 주인은 저장소를 `Fork` 한 사람들의 목록을 볼 수 있다.
-   **B 계정**의 주인은 **A 계정**의 주인에게 내가 한 일, 수정 사항이나 기능이 원본과 병합 할 가치가 있다고 생각하는 이유 등과 함께 `pull request` 를 생성한다.
-   하지만 **B 계정**은 쓰기 권한이 없기 때문에 아직 변동사항은 적용되지 않는다.
-   **A 계정**의 주인은 저장소에서 `pull request` 요청이 들어온 것을 확인할 수 있다.  
    어떠한 메시지를 보냈고, 실제 소스코드까지 전부 비교해서 확인해볼 수 있다.
-   이제 **A 계정**은 `review changes`를 통해 **B 계정**에 대한 피드백과 함께 변경 사항의 병합을 승인할 수 있다.
-   그 이후 `merge pull request - Confirm merge` 를 메모와 함께 클릭하면 병합이 완료된다.
