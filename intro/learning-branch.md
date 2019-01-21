# Git Branch 정리

협업에 있어 가장 중요한 기능 중 하나인 branch를 정리해보겠습니다.


## Branch의 개념
여러 사람이 함께 하나의 프로젝트를 개발하고 있다고 가정합니다. 
누군가는 게시판에 글을 쓰는 기능을 추가하고, 누군가는 회원가입 기능을 추가하고... 
이런식으로 개발을 하다보면 하나의 프로젝트로 각자 다른 버전이 만들어지는 경우가 잦습니다.


이때 사람들이 독립적인 **자신만의 복사본**을 만들어 작업할 수 있도록 하는 것이 바로 branch입니다.
각자 자신만의 즉 복사본을 만들어 작업을 한 후 다른 브랜치와 **병합(merge)** 해가며 작업을 진행해갑니다.


branch를 사용한 작업의 흐름을 잘 보여주는 이미지를 가져왔습니다.
<img src="https://backlog.com/git-tutorial/kr/img/post/stepup/capture_stepup1_1_2.png">


[출처: 누구나 쉽게 이해할 수 있는 Git 입문](https://backlog.com/git-tutorial/kr/img/post/stepup/capture_stepup1_1_2.png)

즉, branch는 커밋 사이를 이동할 수 있는 **포인터** 같은 것입니다. 
Git에는 현재 작업 중인 브랜치를 가리키는 `HEAD`라는 포인터가 존재합니다.


## Branch의 생성과 이동
git init으로 초기화를 하고 나면 자동으로 생겨나는 default branch는 `master` branch입니다. 만약 아무런 branch도 만들지 않는다면 
모든 작업의 흐름은 master 브랜치 안에서 쭉 이어집니다.


진행 중인 프로젝트에 7번 이슈가 생겼다고 가정합니다. 이 이슈를 처리하기 위한 branch를 만듭니다.

```
git branch issue-7
```

현재 존재하는 branch의 목록을 확인해보세요. 현재 선택된 branch는 앞에 `*`이 붙어있습니다.
```
git branch
```
이제 `issue-7`로 이동해봅시다.
```
git checkout issue-7
```

이렇게 하고 나면 `HEAD`는 이제 `issue-7`을 가리키게 됩니다.


branch의 생성과 이동을 한 줄에 처리할 수도 있습니다!
```
git checkout -b issue-7
```

branch를 이동한 상태에서 새로운 commit을 만들어보세요.
```
git commit -m "Move to issue-7"
```

`issue-7` 브랜치는 이제 윗 줄에서 새롭게 만든 commit을 가리키는 포인터가 되었습니다. 여기서 일어난 commit은 다른 branch에는 영향을 주지 않는 별개의 작업입니다.
때문에 `master`는 이 `issue-7`과는 여전히 이전 단계의 commit을 가리키고 있습니다.
다시 `master`로 돌아가보세요.

```
git checkout master
```

프로젝트가 마지막 commit을 하기 전 상태로 돌아가있을 것입니다.


## Branch의 병합과 삭제
다른 branch에서 진행한 작업을 합치기 위해 병합(merge) 작업이 필요합니다.
`issue-7`의 commit 내역을 `master`에 합쳐보겠습니다.

```
git checkout master
git merge issue-7
```

간단합니다. `master`로 돌아가 `git merge [name]` 명령어를 사용하면 됩니다. 이제 두 브랜치는 동일한 commit을 가리키는 포인터가 됩니다.


작업과 병합을 마치고 필요없어진 브랜치는 삭제합니다.
```
git branch -d issue-7
```

## 병합 충돌
병합 작업은 실패할 때도 있습니다. 서로 다른 브랜치가 동일한 부분을 수정한 이력이 있다면 git은 merge를 할 수 없습니다. 
이런 경우를 **충돌(complict)** 이라고 합니다. 충돌이 발생한 파일 목록은 `git status` 명령어로 확인할 수 있습니다.


충돌을 해결하려면 둘 중 한 가지 버전을 선택하거나, merge 도구를 실행해 직접 충돌된 부분을 수정할 수도 있습니다.

```
git mergetool
```

IDE에서 자체적으로 merge 도구를 GUI로 제공하기도 합니다. 제가 지금 쓰고있는 Jetbrains 사의 모든 IDE가 그렇습니다.

충돌을 해결했다면 다시 commit과 merge를 진행하면 됩니다. 여기까지 branch의 기본적인 사용 방법을 정리했습니다.


## Rebase의 개념
사실 branch를 합치는 방법은 merge 외에도 하나가 더 존재합니다. **rebase**입니다.


merge는 두 브랜치의 변경 사항과 공통의 부모를 포함하는 새로운 commit을 만들어냅니다. 
다음 이미지는 merge를 했을 때의 변화를 그림으로 나타낸 것입니다.


<img src="https://git-scm.com/figures/18333fig0328-tn.png" />


[출처 : Git 공식문서](https://git-scm.com/book/ko/v1/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-Rebase%ED%95%98%EA%B8%B0)


rebase도 최종 결과물은 merge와 같지만 그 과정이 조금 다릅니다. 위의 merge의 경우 병합이 2개의 갈래로 나누어져 진행됩니다.
rebase는 이러한 병합 이력을 깔끔하게 한 줄로 만듭니다.

```
git checkout issue-7
git rebase master
```

rebase를 하게 되면, git은 **branch가 나눠지기 전 마지막 commit**부터 **현재 branch까지의 변경사항을 저장**합니다.
그 후 `issue-7`이 `master`가 가리키는 commit을 가리키게 하고, 저장해 놓았던 변경사항을 차례대로 적용합니다. 그림으로 보면 다음과 같습니다.


<img src="https://git-scm.com/figures/18333fig0329-tn.png" />


그리고 `master`가 `issue-7`과 같은 commit을 가리키도록 다시 merge합니다.

```
git checkout master
git merge issue-7
```

<img src="https://git-scm.com/figures/18333fig0330-tn.png" />


히스토리가 한 줄로 깔끔해졌습니다.

여러사람이 각각 다른 작업을 했어도 rebase를 하게되면 모든 작업이 차례대로 수행된 것처럼 보입니다.
따라서 rebase는 리모트 브랜치에 commit을 깔끔하게 적용하고 싶을 때 사용합니다.