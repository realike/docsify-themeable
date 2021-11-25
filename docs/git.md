# Git

**删除本地所有分支**
```
git branch | grep -v "master" | xargs git branch -D
```