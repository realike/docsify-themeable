# Git

## 删除本地所有分支
```
git branch | grep -v "master" | xargs git branch -D
```

## ssh
```
ssh dengweixiong@host -p 15672

ssh-keygen -t rsa -C '861579607@qq.com' -f ~/.ssh/id_rsa

ssh-keygen -m PEM -t rsa -b 4096
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

ref: https://blog.csdn.net/code_segment/article/details/78597441
```

## git拉取远程至本地
```
git checkout --track origin/dev
```

## git撤销最新一次commit
```
git reset --soft HEAD^

git restore --staged . 

ref: https://blog.csdn.net/w958796636/article/details/53611133
```

## git保存账号密码
```
git config --global credential.helper store

git config --local credential.helper store
```

## git代码迁移
```
#从老gitlib拉取裸仓库，并在本地文件系统创建gitbook-demo.git文件夹
git clone --bare ssh://git@oldgitlab:12345/group1/gitbook-demo.git
#进入代码目录
cd gitbook-demo.git
#向新git推送镜像
git push --mirror ssh://git@newgitlab:67890/group1/gitbook-demo.git

参看当前项目的远程仓库地址
git remote -v
# 执行结果：
origin ${old_repo}(push)
origin ${old_repo}(pull)
2.重置项目远程地址

git remote set-url origin ${new_repo}
检查当前origin路径
git remote -v
# 执行结果：
origin ${new_repo}(push)
origin ${new_repo}(pull)
```

## 在当前文件夹下初始化git
```
cd landServer
git init
git remote add origin https://github.com/user/landServer.git
git pull
```