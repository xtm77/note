# git config
## git diff 와 git merge tool을 vscode로 등록하기
```sh
[core]
	editor = code --wait
[diff]
	tool = default-difftool
[difftool "default-difftool"]
	cmd = code --wait --diff $LOCAL $REMOTE
[merge]
	tool = vscode
[mergetool "vscode"]
	cmd = code --wait $MERGED
```