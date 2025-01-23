# git-
<h2>git에 대해서 간단히 알아야 할 지식들을 모아놓았습니다.</h2>


git을 사용하기 위해서는 git window를 다운로드

git default 가 mster로 되어 있다면

`
git config --global init.defaultBranch main 명령어를 이용하면 기본 branch 이름을 바꿀 수 있음
`

`
git branch -M main> vscode에서 이명령어로 기본 이름을 main으로 바꿀 수 있음
`

사용할 폴더에서 shift 우클릭 후 powershell 창열어 컴퓨터에서 git 사용이 처음이면 글러벌 메일과 이름 설정

`
git config --global user.email ~
`

`
git config --global user.name ~
`
vscode 열어 폴더 오픈

작업폴더에 git 을 쓰고 싶다면
터미널 열고 git init 

<b>파일추가</b>

git add 파일명 파일명
git add .

<b>커밋</b>

git commit -m '커밋명'

<b>브랜치 생성</b>

git branch 브랜치명

<b>브랜치 이동</b>

git switch 브랜치명(main)

<b>main 브랜치에 브랜치 합체</b>

git switch main
git merge 합체할 브랜치명 

<b>합체할때</b>

> 기존 메인에 새로운 커밋이 있다면 3-way 머지 진행
> 기존 메인에 새로운 커밋없이 새브랜치만 합쳐지면 fast-forward 머지 진행

<b>머지된 브랜치 삭제</b>

git branch -d 브랜치명

<b>머지 안된 브랜치 삭제</b>

git branch -D 브랜치명

 
브랜치 기록이 너무 더러워 없애고 싶을때 (rebase를 사용해서 main에서 브랜치 뻗어나간 가지를 가장 최근 commit 으로 움직인다음 머지 진행 -> fast forwad를 진행해서 브렌치가 뻣어나지 않은 것처럼 표시)

1. rebase

git switch 없앨브랜치명

git rebase main

git switch main

git merge 없앨브랜치명

2. squash and merge(main 브랜치에서 실행)

git merge --squash 없앨브랜치명

중요한점 > 잔챙이 브런치는 squash 머지 해주세요~ > 로그에 표시될 필요없이 합체

	> feature/develop 브랜치는 3-way 머지해주세요 ~ > 로그 기록에 남게 해주세요.

---
<h3>코드짜다 실수했을때 되돌아가는 법</h3>

1.파일복구 기능
git restore 파일명 > 파일하나에 대해 최근 커밋상태로 되돌림
git restore --source 커밋아이디 파일명 > 특정 commit 시점으로 파일 복구해줌

2.commit 취소하는법
git revert 커밋아이디 > 특정 commit 작업을 취소해줌 (커밋 메세지를 입력하라고 에디터가 뜨는데 입력하고 x 누르면 새로운 commit 이 생성되면서 특정 commit 작업이 취소된다.)
git revert 커밋아이디1 커밋아이디2 > 여러개 동시 취소가능
git revert HEAD >최근 commit 취소해줌
revert 기능으로 merge commit도 취소가 가능하다.

3.과거로 이동기능 
git reset --hard 커밋아이디 > 특정 커밋시점으로 모든걸 되돌린다.(그동안의 모든 기록 삭제)
hard 말고 sort mixed 등이 있다.

이 명령어는 협업시에는 사용을 안하는게 좋다. 주의해야한다!!!


---
내코드 올리기 push
로컬저장소(컴퓨터작업폴더) 에서 원격저장소(온라인 깃헙사이트)에 올리기 위해선 push를 해야함
git push -u 원격저장소주소 올릴로컬브랜치명(main)

또 push하기 위해서는 위 명령어를 사용하면 되는데 원격저장소주소는 기니까 gitd에서 변수문법으로 대체가능하다.

변수 설정
git remote add 변수명 원격저장주소 > 변수명은 관습적으로 origin 으로 한다.


또한 -u 명령어는 원격저장소주소랑 브랜치를 기억해주기 때문에 한번 사용했으면 짧은 명령어로 해결완료
git push 

원격저장소인 github에서 커밋히스토리도 잘 볼 수 있다.
---
타인과 협업하기 git clone, pull
원격저장소 하나를 다른 팀원들이 공동개발하기 위해서는 git clone 원격저장소주소  > 이 명령을 통해 복사해옴 원격저장소에서 공동개발자의 팀원 이름을 추가해 두면 git push를 같이 할 수 있음

원격저장소에 팀원이 push 한 내용이 있으면 로컬저장소에서 push가 불가(파일이 엉킴) , git pull 명령을 통해 한번 당기고 git push 진행

git pull은 git fetch + git merge 임
git fetch : 원격저장소 신규 commit 가져오세요
git merge : 내 브랜치에 merge 

같은 줄을 수정했을 시 conflict 발생할 수 있다.
컴플릭트 발생시 해결방법은 위 앞서 배웠었다.
에디터가 뜨는데 수정하고 커밋하고 하면 알아서 해결된다.

한줄요약 : git push 전에 git pull 하쇼!
---
브랜치로 협업하기 (pull request)
git pull 하고 git push를 하면 되지만 개발자가 많아지면 어지러워진다.
해결방법은 개발자 마다 브랜치를 만들고 merge하는게 좋다.

원격저장소에서도 브랜치만들고 관리가 가능하다.(그러나 로컬에서 만들고 add commit push를 하는게 일방적)

git branch 새브랜치명
git switch 새브랜치명
git add .
git commit -m '커밋명'
git push origin(변수) 새브랜치명  > 새로운 브랜치로 push를 진행(개발자마다 오류방지)

내가 개발한게 작동이 잘되서 내 브랜치를 원격저장소 브랜치(main)에 merge하고싶으면 로컬에서해도 되지만 
협업에서는 깃헙 사이트에서 코드리뷰 등 을 진행한다음 온라인에서 머지하는게 대부분이다.
pull request를 승인하는게 온라인 merge이다.
pull request를 승인하면서 공동작업자들은 커밋내용들을 검토,리뷰 및 댓글작성을 할 수 있다.
온라인 merge도 3가지 방법이 있는데 3-way merge, squah merge rebase merge 에서 원하는걸 선택하면 된다.
다 완료하면 main 브랜치가 새브랜치에서 개발하게 잘 들어온걸 확인 할 수 있다.

요약: 원격저장소도 똑같이 브랜치 만들고 merge(pull request) 가능!
---
git flow / trunk-based 브랜치 전략

코딩노예가 아니라 나중에 팀장도 도맡아서 하고싶다면 알아 두는 것이 좋은 깃흐름 전략이있다.
대표적인 예는 gitflow가 있다.
사진첨부
gitFlow 전략은 크게 5가지로 나뉜다
1.main
2.develop
3.feature
4.release
5.hotfix

develop 브랜치 생성은 프로젝트 사본이다. 팀원들에게 기존 main브랜치를 복사한 develop 브랜치에서 개발을 진행하라고 한다.
팀원들은  신기능 개발을 하기 위해develop브랜치를 복사한 reature 브랜치에서 각각 개발한다. feature/guild 브랜치에서 길드기능을 만들고 feature/friend 브랜치에서 친구기능을 만든다. 완성이 되면 develop브랜치에 merge한다. 중요한 내용이 아니면 squash and merge를 해도 ok
develop에서 만든 2개의 기능이 완성된거 같아도 바로 main에 합치기에 불안하기에 release 브랜치를 또 하나 복사해서 고칠거 고친다.(여기서 테스트나 QA진행 , 테스트서버) 
그 후 완성됐으면  develop 브랜치나 main 브랜치에 merge !! (개발은 계속되야 하니 develop에도 merge)
1.0 mian 브랜치에서 버그를발견 했을시 급하게 버그를 픽스하기 위해서 hotfix 브랜치를 통해 바로바로 버그 수정
버그가 잡혔으면 1.0.1 로 main과 develop에 merge!!!

두번째로 Trunk-based 전략
대충 코드짠걸로 바로바로 배포해도 상관없는 프로그램이면 대격변이 없다면 굳이 많은 브랜치를 만들 필요가 없다.

사진첨부

1.기능추가, 버그 픽스가 필요하면 main 브랜치에서 새로운 브랜치를 만들어 코드를 짠다. (작명 잘하는게 중요)
2.기능이 완성되면 main 브랜치에 합침(브랜치는 쓸데없으니 삭제 ㅇ)
3.main 브랜치에 있는 코드를 필요할때마다 유저들에게 배포

장점은 코드를 한 브랜치에서만 관리하기때문에 편리하다
그러나 코드리뷰를 자주해야된다

마지막으로 merge할때 방법차이
기록을 남겨야하는 중요한 브랜치를 merge할땐 3-way merge
기록을 남길 필요없는 쓸데없는 브랜치를 merge할때 squash,rebase merge
---
git stash로 코드 잠깐 보관하기

커밋을 한 이후 코드를 작성하다가 지금까지 작성한 코드(커밋이후부터 지금)를 따로 임시저장하고 싶을때
git stash

메모남기고 따로 저장할땐
git stash save '메모'

보관코드 보는 명령
git stash list

보관함에서 삭제
git stash drop 번호 (1개)
git stash clear (전부)

보관함에서 가져올 때 
git stash pop > 가장 최근에꺼 가져옴


주석처리하면 되는데 왜사용하냐
> 나중에 commit할때 반영이 되서 쓸데없는거 지우기 위해선 stash 기능을 쓴다.
