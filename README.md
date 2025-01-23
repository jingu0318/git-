# Git 사용 가이드

## 깃에 모든 것

1. **Git 설치**
   - git window를 다운로드합니다.
   - 기본 브랜치 이름을 변경하려면 아래 명령어를 사용합니다.
     ```bash
     git config --global init.defaultBranch main
     ```
   - Visual Studio Code에서 기본 이름을 `main`으로 변경하려면 아래 명령어를 사용합니다.
     ```bash
     git branch -M main
     ```

2. **Git 초기 설정**
   - 사용할 폴더에서 Shift + 우클릭 후 PowerShell 창을 엽니다.
   - 컴퓨터에서 Git 사용이 처음이라면 글로벌 메일과 이름을 설정합니다.
     ```bash
     git config --global user.email "이메일"
     git config --global user.name "이름"
     ```

3. **Visual Studio Code 열기**
   - 폴더를 오픈합니다.

4. **작업 폴더에서 Git 사용하기**
   - 터미널을 열고 아래 명령어로 Git을 초기화합니다.
     ```bash
     git init
     ```

5. **파일 추가**
   - 파일을 추가하려면 아래 명령어를 사용합니다.
     ```bash
     git add 파일명
     git add .
     ```

6. **커밋**
   - 커밋하려면 아래 명령어를 사용합니다.
     ```bash
     git commit -m '커밋명'
     ```

7. **브랜치 관리**
   - 브랜치 생성:
     ```bash
     git branch 브랜치명
     ```
   - 브랜치 이동:
     ```bash
     git switch 브랜치명
     ```
   - 메인 브랜치에 브랜치 합체:
     ```bash
     git switch main
     git merge 합체할 브랜치명
     ```

8. **머지 시 주의 사항**
   - 기존 메인에 새로운 커밋이 있다면 3-way 머지가 진행됩니다.
   - 기존 메인에 새로운 커밋 없이 새 브랜치만 합쳐지면 fast-forward 머지가 진행됩니다.

9. **브랜치 삭제**
   - 머지된 브랜치 삭제:
     ```bash
     git branch -d 브랜치명
     ```
   - 머지되지 않은 브랜치 삭제:
     ```bash
     git branch -D 브랜치명
     ```

10. **브랜치 기록 정리**
    - 1. Rebase
      ```bash
      git switch 없앨브랜치명
      git rebase main
      git switch main
      git merge 없앨브랜치명
      ```
    - 2. Squash and Merge
      ```bash
      git merge --squash 없앨브랜치명
      ```

## 코드 수정 및 되돌리기

1. **파일 복구 기능**
   - 최근 커밋 상태로 되돌리기:
     ```bash
     git restore 파일명
     ```
   - 특정 커밋 시점으로 파일 복구:
     ```bash
     git restore --source 커밋아이디 파일명
     ```

2. **커밋 취소하는 법**
   - 특정 커밋 작업을 취소:
     ```bash
     git revert 커밋아이디
     ```
   - 여러 개 동시 취소:
     ```bash
     git revert 커밋아이디1 커밋아이디2
     ```
   - 최근 커밋 취소:
     ```bash
     git revert HEAD
     ```

3. **과거로 이동 기능**
   - 특정 커밋 시점으로 모든 것을 되돌리기:
     ```bash
     git reset --hard 커밋아이디
     ```

**주의:** 이 명령어는 협업 시 사용하지 않는 것이 좋습니다.

## 내 코드 올리기

1. **Push**
   - 로컬 저장소에서 원격 저장소에 올리기:
     ```bash
     git push -u 원격저장소주소 올릴로컬브랜치명
     ```

2. **변수 설정**
   - 원격 저장소 주소를 변수로 설정:
     ```bash
     git remote add 변수명 원격저장주소
     ```

3. **Push 간편화**
   - 이후에는 아래 명령어로 간편하게 Push 할 수 있습니다.
     ```bash
     git push
     ```

## 협업하기

1. **Git Clone, Pull**
   - 원격 저장소 복사:
     ```bash
     git clone 원격저장소주소
     ```
   - 원격 저장소에서 팀원이 Push한 내용이 있을 경우 Pull:
     ```bash
     git pull
     ```

2. **Conflict 발생 시**
   - 에디터가 뜨면 수정 후 커밋하여 해결합니다.

**요약:** Git Push 전에 반드시 Git Pull을 하세요!

## 브랜치로 협업하기 (Pull Request)

1. **브랜치 생성 및 관리**
   - 새로운 브랜치 생성 및 Push:
     ```bash
     git branch 새브랜치명
     git switch 새브랜치명
     git add .
     git commit -m '커밋명'
     git push origin 새브랜치명
     ```

2. **Pull Request**
   - 코드 리뷰 후 Pull Request를 승인하여 Merge합니다.

## Git Flow / Trunk-Based 브랜치 전략

1. **Git Flow**
   - 브랜치 구조: `main`, `develop`, `feature`, `release`, `hotfix`
   - 각 브랜치의 역할을 명확히 구분합니다.

2. **Trunk-Based 전략**
   - 기능 추가 및 버그 픽스 시, main 브랜치에서 새 브랜치를 만들어 작업 후 바로 합칩니다.

## Git Stash로 코드 잠깐 보관하기

1. **코드 임시 저장**
   - 코드 임시 저장:
     ```bash
     git stash
     ```

2. **메모 남기고 저장**
   - 메모와 함께 저장:
     ```bash
     git stash save '메모'
     ```

3. **보관 코드 보기**
   - 보관 목록 확인:
     ```bash
     git stash list
     ```

4. **보관함에서 삭제**
   - 특정 항목 삭제:
     ```bash
     git stash drop 번호
     ```
   - 모든 항목 삭제:
     ```bash
     git stash clear
     ```

5. **보관함에서 가져오기**
   - 가장 최근의 것을 가져오기:
     ```bash
     git stash pop
     ```
