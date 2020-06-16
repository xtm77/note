# Git 사용 흐름
* 프로젝트의 git 브랜치는 master, develop, release, feature, hotfixes로 나눈다.
1. git 저장소 생성
```sh
mkdir myproject
cd myproject
git init
echo "# My Project" >> README.md
git add README.md
git commit -m "first commit"
```

2. 원격 저장소 연결
```sh
git remote add origin https://github.com/xtm77/study.git
git push origin master
```

3. develop 브랜치 생성
```sh
git branch develop
git checkout develop
```
or
```sh
git checkout -b develop
```
> git checkout -b는 브랜치를 생성하고 생성한 브랜치로 이동한다.

then
```sh
git push origin develop
git branch --set-upstream-to origin/develop
Branch 'develop' set up to track remote branch 'develop' from 'origin'
```
or
```sh
git push -u origin develop
```
> 개발 브랜치를 원격 저장소에 생성하고  
> 생성된 원격 저장소의 개발 브랜치와 로컬 저장소의 브랜치를 연결한다.  

4. 기능별 브랜치 생성
> 개발을 하기 위해 새로운 브랜치를 생성할 때는 develop 브랜치로 부터 생성한다.  
> 기능별로 브랜치를 생성하고 같은 기능을 개발 하는 개발자가 여러 명일 경우 기능별 브랜치에서 개발자 별로 브랜치를 생성한다.  

> 아래 예제는 file-management라는 기능을 개발하기 위해 새로운 브랜치를 생성하는 과정을 설명한다.  
```sh
git checkout develop
git checkout -b feature/file-management
git push origin feature/file-management
git branch -u origin/feature/file-management
```
> -u 옵션은 --set-upstream-to 와 같다.

5. 여러 개발자들가 같은 기능을 개발하는 경우
> 특정 기능을 1명이 개발할 때는 별도 브랜치를 생성하지 않아도 된다.  
> 개발자가 여러 명일 경우 기능별 브랜치에서 개발자 별로 브랜치를 생성한다.  
> feature/file-management-dev1, feature/file-management-dev2 같이 분리하여 개발한 후 feature/file-management 브랜치에 병합한다.  
```sh
git checkout feature/file-management
git branch feature/file-management-dev1
git checkout feature/file-managemen-dev2
```
> 필요한 경우 원격 저장소에 브랜치를 생성한다.  
> 개발자별로 브랜치를 계속 만들 경우 브랜치 목록이 지저분해지고 관리가 하기 어려워 진다.  
> 부모 브랜치인 feature/file-management에 병합하여 원격 저장소에 공유하는 것이 낫다.  
```sh
git push origin feature/file-management-dev1
git branch -u origin/feature/file-management-dev1
```

6. 개발 소스 커밋
> 새로 파일을 만들거나, 수정하거나, 삭제한 후 반영한다.
```sh
git add *
git commit -m "파일관리기능 개발"
git push
```

7. 소스 병합하기
> 기능 개발이 완료 된 후 develop 브랜치(이하 개발 브랜치)에 병합하는 작업을 진행한다.  
```sh
git checkout develop
git merge feature/file-management
git push
```
> 병합을 하면 fast-forward, auto-merging, conflict 상황이 발생한다. conflict가 발생할 경우 담당 개발자들과 같이 수정해야 할 수도 있다.  
> git push 할 때 origin feature/file-management 가 생략될 수 있다.  

> 개발 중에는 4, 5, 6, 7번이 반복된다.  
> 여러 기능을 동시에 개발이 진행될 때 전체 기능에 문제가 없을 경우 MSA에서는 짧은 개발 기간과 잦은 배포를 권장하고 있으므로 먼저 개발된 기능을 병합하고 배포하는 것도 고려해 보는 것이 좋다.  

8. 배포준비하기
> 기능 개발이 완료되어 배포한다. 개발 브랜치로 이동한 후 릴리즈 브랜치를 생성하고, 태그를 생성한다.  
```sh
git checkout develop
git checkout -b release/1.0
git push origin release/1.0
git branch -u origin/release/1.0
```
> 배포 준비 중에 변경이 발생한 경우 변경한 내용을 개발 브랜치에 병합한다.  

```sh
git checkout develop
git merge release/1.0
git push
```

> 배포 준비가 완료되면 master 브랜치에 릴리즈 브랜치를 병합한다.  
```sh
git checkout master
git merge release/1.0
```

> master 브랜치에 병합한 후 태그를 추가한다.  
```sh
git tag -a 1.0 -m "1.0 릴리즈"
git push origin 1.0
```

> 태그된 소스를 git 서버로 부터 받아 운영서버로 반영한다.  

9. 배포 버전의 긴급 수정 배포
> 릴리즈 1.0이 버그로 인해 수정되어야 하는 경우 hotfixes 접두어로 브랜치를 생성한다.  
```
git checkout -b hotfixes/1.1
git push origin hotfixes/1.1
git branch -u hotfixes/1.1
```

> 릴리즈된 master로 부터 hotfixes/1.1 브랜치를 생성하여 수정 후 master와 develop 브랜치에 병합해야 한다.  

```
git checkout develop
git merge hotfixes/1.1
git push

git checkout master
git merge hotfixes/1.1
git push
```
