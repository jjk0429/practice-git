Git 연습장
==========

:octocat: 이곳은 git에 처음 입문하는 수정이들이 자유롭게 `commit, pull request, push, branch` 등을 연습해보는 repository입니다.

> 이 가이드 문서는 git의 매우 기초적인 기능만을 다루고 있기 때문에 보충하고 싶으신 내용이 있거나 오류를 발견하셨다면 언제든 수정해주세요.

이용 규칙
---------

1.	이 프로젝트로 git과 github를 학습하는 수정이들은 **어떤 내용이든 좋으니**\(*내 좌우명이 적힌 .txt 파일, 오늘 읽은 책 독후감, Hello world 출력하는 .c 파일 등*) 궁금한건 뭐든 실험(?)해보고 자유롭게 기여를 해주세요!
2.	다른 사람이 작성한 파일은 삭제하지 말아주세요.
3.	commit message는 본인이 어떤 일을 했는지 의미를 담아서 간결하게 작성해주세요.

`나쁜 예) 190130 김뽀룡, 아 이게 왜 안되지, 이 메세지는 영국에서 시작되었으며...`

기본 개념
---------

#### git은 무엇인가요?

git은 간단하게 말해 `버전 관리 시스템(VCS - Version Control System)`입니다. 리눅스 운영체제를 개발한 리누스 토발즈가 개발해 세계적으로 가장 많이 쓰이는 소스관리 툴이예요. git을 사용하면 프로젝트를 체계적으로 관리하는데 큰 도움이 됩니다.

#### 버전 관리는 무엇인가요?

수정님들은 평소 팀 프로젝트를 할 때 과제물을 어떻게 관리하셨나요? 아직 git을 사용해보지 않으셨다면 보통은 파일을 zip으로 압축해 카카오톡, 이메일, 드라이브 등으로 공유하셨을 거라고 생각합니다.

```
프로젝트_최종.zip
최종의_최종.zip
진짜_마지막_최종.zip
진짜_리얼_마지막_최종.zip
```

규모가 작은 프로젝트라면 그런 방식으로도 큰 문제가 생기지 않을 수 있겠지만, 많은 사람들이 공동으로 작업하는 대형 프로젝트에서 그런 식으로 프로젝트 소스를 관리하면 엄청난 혼란이 발생하게 됩니다.��

그래서 도입된 것이 바로 `버전 관리 시스템`입니다. 버전 관리 시스템은 파일의 변화를 시간에 따라 기록하여 과거 특정 시점의 버전을 다시 불러올 수 있게 해줍니다. 버전 관리 시스템에는 여러가지 종류가 있는데요, git은 그 중에서도 `분산 모델`에 속합니다!

시작 가이드
-----------

1.	우선 git을 설치해야 합니다. 링크로 들어가 본인의 운영체제에 맞게 다운받으시면 됩니다. 설치 방법은 생략할게요. [(설치링크)](https://git-scm.com/downloads)
2.	내 컴퓨터에서 원하는 위치에 `마우스 우클릭` 후 `Git Bash Here`을 클릭합니다. ![img1](https://github.com/DevSungshin/practice-git/blob/master/intro/img1.png?raw=true)
3.	bash 창이 나타났다면 최초 설정이 필요합니다. 이건 처음 한 번만 해주면 됩니다. `git config` 명령어로 사용자의 이름과 이메일 주소를 설정해주세요.

```
  git config --global user.name "본인 이름"
  git config --global user.email "본인 이메일"
```

여기서 입력된 정보는 앞으로의 commit 때마다 사용됩니다.

1.	**현재 위치를 git 저장소로 초기화** 하기 위해 `git init` 명령어를 입력해주세요. 그러면 **.git** 폴더가 생성됩니다.

2.	이제 작업을 하기 위해 이 저장소(repository)의 내용물을 수정님의 로컬 컴퓨터로 다운 받아야합니다. 이때 사용하는 명령어는 **복제한다는 의미를 담은** `git clone [project url]`입니다.

```
  git clone https://github.com/DevSungshin/practice-git.git
```

![img2](https://github.com/DevSungshin/practice-git/blob/master/intro/img2.png?raw=true)

잠시 기다리면 practice-git이라는 폴더가 생성되고 안에는 이 repository의 내용이 그대로 들어있는 것을 확인할 수 있습니다. 이제 본격적으로 작업할 준비가 되었네요.

1.	경로를 변경하는 명령어 `cd`를 사용해서 작업할 폴더 안으로 들어가주세요.

```
  cd practice-git
```

새로운 파일을 추가하거나, 기존 파일을 수정합니다. 저는 예시로 practice 폴더 안에 *hi.txt* 파일을 만들어볼게요!

1.	`git status` 명령어로 저장소의 상태를 출력해보세요. Untracked files 목록에 내가 변경 혹은 수정한 내역이 붉은 글자로 뜬다면 git이 제대로 프로젝트의 **변경사항을 추적하고 있다는 뜻** 입니다.

![img3](https://github.com/DevSungshin/practice-git/blob/master/intro/img3.png?raw=true)

1.	그러면 이제 `git add [name]` 명령어로 저장소에 파일을 추가합니다. 특정 파일이나 디렉터리 전체를 추가할 거라면 뒤에 이름을 그대로 써주면 되고, 모든 변경 사항을 add 할거라면 `git add *`을 입력해주세요.

```
  git add *
  git add practice
```

변경사항이 하나뿐인 이 경우 저 두 개의 명령어는 같은 기능을 하겠네요! 다시 한 번 git status 명령어로 저장소 상태를 출력해보세요.

![img4](https://github.com/DevSungshin/practice-git/blob/master/intro/img4.png?raw=true)

1.	이 상태에서 실제 변경 내역을 **확정** 하려면 `git commit` 명령어를 사용해야 합니다.

add와 commit의 차이가 뭔지 처음에는 헷갈릴 수 있습니다. add는 저장소에 `변화를 반영`시키는 것이고, commit은 `일정한 작업의 단위를 확정`하는 것이라 생각하면 됩니다. commit을 하고나면 마지막 commit 이후부터 현재까지 발생한 모든 변경사항을 모아 새로운 버전을 만들게 됩니다. 즉, **'commit = 버전을 만든다.'** 라고 생각하시면 됩니다.

이러한 commit에는 내가 어떤 작업을 했는지 설명하는 **메세지** 가 필요합니다. 메세지는 `-m` 옵션으로 설정합니다.

```
  git commit -m "이번 작업에 대한 설명"
```

1.	이제 마지막 단계입니다! 지금까지의 작업 내역을 원격 저장소(=리모트 저장소)에 반영시켜야겠죠? commit 내역을 원격 저장소로 보내는 명령어는 `git push [리모트 저장소 이름] [브랜치 이름]` 입니다. 브랜치는 `작업의 흐름`이라 생각하면 되는데, 당장은 몰라도 되므로 설명은 생략하겠습니다.

리모트 저장소의 기본 이름은 origin, 기본 브랜치 이름은 master이므로 다음과 같이 입력합니다.

```
  git push origin master
```

지금까지의 작업이 정상적으로 진행되었다면 bash 창에는 다음과 같이 표시됩니다.

![img5](https://github.com/DevSungshin/practice-git/blob/master/intro/img5.png?raw=true)

이제 github로 다시 돌아와보니 방금 push한 내용이 반영 되어있네요!

![img6](https://github.com/DevSungshin/practice-git/blob/master/intro/img6.png?raw=true)

#### 지금까지 진행한 [작업 - add - commit - push]의 흐름을 반복하는 것이 git 활용의 대부분을 차지합니다. 당장은 적응되지 않아도 반복하다보면 자연스럽게 익숙해집니다.

### 일단은 그냥 많이 써보세요! ��

더 많은 정리글
--------------

-	[Git branch 정리](https://github.com/DevSungshin/practice-git/blob/master/intro/learning-branch.md)
-	[Git fetch와 pull 정리](https://github.com/DevSungshin/practice-git/blob/master/intro/fetch-and-pull.md)

-	추천 학습 사이트
	----------------
-	[공식 문서 (한글)](https://git-scm.com/book/ko/v2)

-	[누구나 쉽게 이해할 수 있는 Git 입문](https://backlog.com/git-tutorial/kr/intro/intro1_1.html?fbclid=IwAR0i2cl1khBuMez9FaWISUBsUN-2DvI5h_lWwnYYRlk4BHAQEnAzKxh8qRQ)

-	[git을 시작하기 위한 간편 안내서](https://rogerdudler.github.io/git-guide/index.ko.html)

-	[직접 따라해보면서 git을 실습하는 웹사이트](https://learngitbranching.js.org/)

-	[생활코딩 Git 강의](https://opentutorials.org/course/2708)

추천 도서
---------

> 중앙도서관 6층에 있는 책만 추가했습니다. 다른 좋은 책을 알고 계신다면 이어서 써주세요.��

-	[프로 Git](http://lib.sungshin.ac.kr/search/detail/CATTOT000000586256?mainLink=/search/tot&briefLink=/search/tot/result?q=git_A_service_type=brief_A_q2.y=0_A_st=KWRD_A_q2.x=0_A_si=TOTAL)
-	[인간다운 Git](http://lib.sungshin.ac.kr/search/detail/CATTOT000000653876?mainLink=/search/tot&briefLink=/search/tot/result?q=git_A_service_type=brief_A_q2.y=0_A_st=KWRD_A_q2.x=0_A_si=TOTAL)
	-	git의 아주 기본적인 개념부터 풀어서 설명하는 책이라 초심자 분께 추천드립니다. 두께가 얇아서 금방 읽을 수 있어요.
-	[Git GitHub 입문](http://lib.sungshin.ac.kr/search/detail/CATTOT000000617055?mainLink=/search/tot&briefLink=/search/tot/result?q=git_A_service_type=brief_A_q2.y=0_A_st=KWRD_A_q2.x=0_A_si=TOTAL)
	-	git 뿐만 아니라 github의 사용 방법까지 함께 설명해주는 책입니다.
