Git pull과 fetch
================

`commit`과 `push`로 나의 작업 내역을 원격 저장소(리모트 저장소)에 반영시킬 수 있다면, 반대의 역할을 하는 명령어도 필요하겠죠?

이 글에서 소개할 `fetch`와 `pull`는 **원격 저장소의 내용을 로컬로 가져올 때** 사용하는 명령어입니다.

### 원격 저장소 확인과 추가

만약 프로젝트를 `git clone`으로 가져왔다면 `origin`이라는 이름의 원격 저장소 주소가 자동으로 추가되어 있습니다. 그 외에 로컬 저장소와 동기화 하고 싶은 원격 저장소가 있다면 직접 추가해야합니다.

`git remote` 명령어로 현재 등록된 원격 저장소의 리스트를 볼 수 있습니다.

```
git remote
```

`-v` 옵션으로 주소까지 함께 출력할 수 있습니다.

```
git remote -v
```

프로젝트에 새로운 원격 저장소를 추가한다면 다음과 같이 작성하면 됩니다.

```
git remote add [remote-name] [url]
git remote add upstream https://github.com/DevSungshin/study-algorithm
```

`show` 명령어로 remote의 정보를 확인할 수 있습니다.

```
git remote show [remote-name]
git remote show origin
```

### Git pull 사용하기

`pull` 명령어는 원격 저장소의 데이터를 로컬 저장소에 반영시킵니다.

```
git pull
```

원격 저장소와 로컬 저장소의 새로운 변경 사항이 서로 겹치지 않는다면 곧바로 병합이 이루어집니다. 결과적으로 로컬 저장소의 `master` 브랜치와 리모트 저장소 `origin`의 `origin/master`가 같은 commit을 가리키게 됩니다.

하지만 만약 **원격 저장소와 로컬 저장소가 같은 파일을 수정한 이력**이 있다면, **병합 충돌** 이 발생하게 됩니다. 이때는 사용자가 직접 충돌난 부분을 merge 도구로 수정하여 다시 한 번 병합을 해야합니다.

### Git fetch 사용하기

`pull`은 원격 저장소의 변경 사항을 자동으로 기존의 프로젝트와 병합합니다. `fetch`는 원격 저장소의 내용을 로컬 저장소로 가져온 후 병합은 하지 않습니다.

동기화할 원격 저장소의 이름을 입력해야합니다.

```
git fetch [remote-name]
```

간단하게, `pull`에서 `merge`를 생략했다고 생각하면 됩니다. `fetch`로 받아온 내역을 병합하려면 `merge` 또는 `pull` 하면 됩니다.

`fork`했던 다른 사람의 저장소를 최신 버전으로 업데이트할 때 내용 검토가 필요할 경우 `fetch`를 사용합니다.
