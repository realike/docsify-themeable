# Git

## 删除本地所有分支
```
git branch | grep -v "master" | xargs git branch -D
```

## ssh
```
ssh dengweixiong@host -p 15672

ssh-keygen -t rsa -C '861579607@qq.com' -f ~/.ssh/id_rsa
```

## git config
```
git config --global user.name "realike"
git config --global user.email "861579607@qq.com"
git config --global --list

git config --global pager.branch false
git config --global pager.stash false
```

## git多账户配置 
```
git config --local user.name "realike"
git config --local user.email "861579607@qq.com"
git config --local --list

vim ~/.ssh/config

# aliyun
Host codeup.aliyun.com
HostName codeup.aliyun.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
# github
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa

ssh -T git@codeup.aliyun.com
ssh -T git@github.com
```

## git回退
场景
本来想把github上的newpbft合并到本地的newpbft分支上，由于没有查看当前分支，直接运用git pull origin newpbft，结果将newpbft合并到了master分支中
```
git reflog

git reset --hard
```

## git拉取远程至本地
```
git checkout --track origin/dev
```
