# Git

**删除本地所有分支**
```
git branch | grep -v "master" | xargs git branch -D
```

**ssh**
```
ssh dengweixiong@host -p 15672

ssh-keygen -t rsa -C '861579607@qq.com' -f ~/.ssh/id_rsa
```

**git config**
```
git config --global user.name "realike"
git config --global user.email "861579607@qq.com"
git config --global --list
```

**git多账户配置**
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