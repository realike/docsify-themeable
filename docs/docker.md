# Docker

## install
```
https://docs.docker.com/engine/install/ubuntu/

https://www.jiebaiyou.com/2020/06/05/Windows-10-WSL2-%E5%AE%89%E8%A3%85%E4%BD%BF%E7%94%A8%E5%8F%8ADocker%E5%AE%89%E8%A3%85/

# 启动 docker 守护进程
sudo service docker start
# 运行测试
sudo docker run hello-world

sudo service docker restart

```

## 镜像
```
https://cr.console.aliyun.com/eu-central-1/instances/mirrors

sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://yp87mt7e.mirror.aliyuncs.com"]
}
EOF

sudo service docker restart

docker info
```

## 命令 
```
查看所有的容器
docker ps -a

启动一个已停止的容器
docker start

进入容器
docker exec -it

清除终止状态容器
docker container prune
```
```
docker中 启动所有的容器命令
docker start $(docker ps -a | awk '{ print $1}' | tail -n +2)

docker中 关闭所有的容器命令
docker stop $(docker ps -a | awk '{ print $1}' | tail -n +2)

docker中 删除所有的容器命令
docker rm $(docker ps -a | awk '{ print $1}' | tail -n +2)

docker中 删除所有的镜像
docker rmi $(docker images | awk '{print $3}' |tail -n +2)

echo "aa bb cc" | awk -F '{print $1}' 结果就是aa，意思是把字符串按空格分割，取第一个。
awk 是用来提取列的主要工具；
{print $1} 就是将某一行（一条记录）中以空格为分割符的第一个字段打印出来。
```