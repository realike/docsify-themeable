# Go

## go env
```
go env -w GOPROXY=https://goproxy.cn

go env -w GO111MODULE=on
warning: go env -w GO111MODULE=... does not override conflicting OS environment variable --> 修改对应的export GO111MODULE=on   

command not found: shopt .....
if use zsh, that not source ~/.bashrc, source ~/.zshrc

```

```
curl: (7) Failed to connect to raw.githubusercontent.com port 443: Connection refused

打开  https://www.ipaddress.com/ 输入访问不了的域名，获得对应的IP。

使用vim /etc/hosts命令打开不能访问的机器的hosts文件，添加如下内容：
199.232.68.133 raw.githubusercontent.com
199.232.68.133 user-images.githubusercontent.com
199.232.68.133 avatars2.githubusercontent.com
199.232.68.133 avatars1.githubusercontent.com
```