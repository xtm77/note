# Git
## 활용
### Commit 취소하기

#### Staged 상태로 취소하기
```
git log --oneline
git reset --soft HEAD^
```

#### Unstaged 상태로 취소하기
```
git log --oneline
git reset --mixed HEAD^
# or
git reset HEAD^
# or 마지막 2개 commit 취소
git reset HEAD~2
```

#### Commit 취소 및 삭제
```
git reset --hard HEAD^
```




