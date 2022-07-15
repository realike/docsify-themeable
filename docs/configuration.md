# Config

## oh-my-zsh
```go
https://sysin.org/blog/linux-zsh/

https://zhuanlan.zhihu.com/p/351281543

https://www.kancloud.cn/ichenpeng/blog/1096725

// add path to .zshrc

//  取消下划线
ZSH_HIGHLIGHT_STYLES[path]=none
ZSH_HIGHLIGHT_STYLES[path_prefix]=none

// theme vim ~/.zshrc
ZSH_THEME="dst"

// alias
cat ~/.oh-my-zsh/plugins/git/git.plugin.zsh

source ~/.zshrc
```

```shell
# zsh history
sudo npm install -g zsh_history

zsh_history
```

## redis 
```go
ps -ef | grep redis

kill -9 ${pid}

// wsl2 redis start
sudo service redis-server start
```

## profile 
```
 /etc/profile，/etc/bashrc 是系统全局环境变量设定 
 ~/.profile，~/.bashrc用户家目录下的私有环境变量设定 
 当登入系统时候获得一个shell进程时，其读取环境设定档有三步 
 1首先读入的是全局环境变量设定档/etc/profile，然后根据其内容读取额外的设定的文档，如 
 /etc/profile.d和/etc/inputrc 
 2然后根据不同使用者帐号，去其家目录读取~/.bash_profile，如果这读取不了就读取~/.bash_login，这个也读取不了才会读取 
 ~/.profile，这三个文档设定基本上是一样的，读取有优先关系 
 3然后在根据用户帐号读取~/.bashrc 
 至于~/.profile与~/.bashrc的不区别 
 都具有个性化定制功能 
 ~/.profile可以设定本用户专有的路径，环境变量，等，它只能登入的时候执行一次 
 ~/.bashrc也是某用户专有设定文档，可以设定路径，命令别名，每次shell script的执行都会使用它一次
```

## go安装
```shell
sudo tar -C /usr/local -xzf go1.14.linux-amd64.tar.gz

use ~/.zshrc 添加覆盖~/.bashrc
export GOROOT=/usr/local/go
export GOPATH=/home/dwx/go
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
export GO111MODULE=on
export GOPROXY=https://goproxy.cn

在GOPATH下创建
mkdir bin && mkdir pkg && mkdir src

# 新项目配置
src -> git clone -> go mod tidy
vscode -> wsl插件 -> Go:Install/Update Tools(ctr+shift+p)

# ref
注: 查看go工程项目结构的问题(GOPATH问题, 以及用来GO module后不再需要GOPATH ref: [1, 2])
1: https://www.flysnow.org/2021/05/15/install-golang.html
2: GOPATH GOROOT 工程目录区别 https://www.cnblogs.com/zhaof/p/7906722.html
3: https://www.v2ex.com/t/799639
4: https://www.cnblogs.com/zhaojingyu/p/9008877.html

finally: https://www.cnblogs.com/wjaaron/p/14797003.html
manage go version: https://github.com/owenthereal/goup
```

## wsl2安装
```shell
##手动安装  
https://docs.microsoft.com/zh-cn/windows/wsl/install-manual

# 命令  
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

重启Windows

https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

wsl --set-default-version 2


## 自动安装  
https://docs.microsoft.com/zh-cn/windows/wsl/install



## Ubuntu 20.04设置  
https://docs.microsoft.com/zh-cn/windows/wsl/setup/environment#set-up-your-linux-user-info

sudo passwd root
```


