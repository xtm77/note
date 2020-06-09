# Git Branch
## Git Branch Types

1. master
    > 제품 출시를 위한 브랜치
    > tag를 붙여 버전으로 관리
    > 배포 가능한 상태만 관리
    > release 브랜치를 가져와 병합

2. develop
    > 다음 출시 버전을 개발하는 브랜치
    1. 기능 개발을 위한 브랜치들을 병합하기 위해 사용
    2. 모든 기능이 추가되고 버그가 수정되어 배포 가능한 안정적인 상태에서 master 브랜치로 병합
    3. 평소에는 이 브랜치를 기반으로 개발을 진행
    4. feature 브랜치를 이 브랜치에서 생성
    5. feature 브랜치를 가져와 병합
    6. release 브랜치로 병합 됨

3. release
    > 버전 출시를 준비하는 브랜치
    1. develop 브랜치를 가져와 병합
    2. release 브랜치를 master에 병합한 후 다시 develop으로 병합(* master로 병합하는 중에도 develop은 계속 개발 중일 것이므로 develop으로 release를 병합해야 함)
    3. release -> master, release -> develop

4. feature
    > 기능을 개발하는 브랜치
    1. develop 브랜치로부터 생성
    2. 기능이 개발이 완료된 후에 develop으로 병합

5. hotfixes
    > 배포 전에 master에 버그가 발견된 경우 긴급하게 수정하는 브랜치
    1. master로 부터 생성
    2. 수정 완료 후에 master와 develop로 병합
--- 
> 위까지는 Git-flow에서 사용되는 브랜치 종류
---
6. issue
    > 개발 중에 발생한 버그를 수정하는 브랜치

---

## Git Branch Work Flow
![GitFlowBranches](../images/gitflow.png)


## Git Branch

### 협업을 위한 브랜치 사용

* 협업규칙
    1. master 브랜치에는 직접 커밋하지 않는다.
    2. 개발 전 master 브랜치 기준으로 새로운 브랜치를 만든다.
    3. 브랜치 이름은 적당한 형식(예: feature/기능이름)으로 한다.
    4. 해당 브랜치는 한 명만 커밋한다.
    5. 해당 브랜치에서 기능 개발이 끝나면 master 브랜치와 병합한다.

+ 브랜치 생성하기
    ```sh
    git checkout -b mybranch
    ```
    > checkout은 브랜치 생성 및 이동하는 명령. 아래의 두 명령줄을 한번에 실행함.
    ```sh
    git branch mybranch
    git checkout mybranch
    ```

+ 브랜치 삭제
    ```sh
    git branch --delete mybranch
    git branch --d mybranch
    ```

    커밋한 이력이 남아 있어 브랜치가 삭제되지 않을 경우 아래와 같이 강제로 삭제
    ```sh
    git branch -D mybranch
    ```

    원격에 있는 브랜치를 삭제
    ```sh
    git push origin :mybranch
    ```

+ 브랜치 목록 보기
    ```sh
    $ git branch
    develop
    feature/git
    * master
    release
    ```

    ```sh
    $ git branch -vv
    develop     4501767 Git Ignore file 추가
    feature/git 4501767 [origin/feature/git: ahead 1] Git Ignore file 추가
    * master      4501767 [origin/master] Git Ignore file 추가
    release     4501767 Git Ignore file 추가
    ```

+ 로컬저장소 브랜치를 원격저장소에 생성
    ```sh
    git push origin mybranch
    ```
+ 로컬저장소 브랜치를 원격저장소 브랜치와 연동
    ```sh
    git branch --set-upstream-to origin/mybranch
    ```
    or
    ```sh
    git branch -u origin/mybranch
    ```
+ 브랜치 이동
    ```sh
    git checkout mybrach
    git checkout master
    git checkout develop
    ```
+ git switch와 git restore
    > checkout이 2.23.0 이후로 switch와 restore로 분리되었다.
    - git switch = git checkout <브랜치>
        > git switch는 브랜치를 변경
    - git restore = git checkout -- <파일명>
        > git restore는 파일을 복원
## 프로젝트 기본 브랜치들
* 종류
    - master
    - develop
    - release/
    - feature/
    - hotfixes/
