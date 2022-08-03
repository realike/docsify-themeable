# temp

##
```
栈:
    辅助栈

链表:
    反转
    哈希
    回溯
```

一、限制VM的内存使用

按下Windows + R 键，输入 %UserProfile% 并运行进入用户文件夹
新建文件 .wslconfig ，然后使用记事本编辑
填入以下内容并保存, memory为wsl2分配的内存上限，可根据自身电脑配置设置
[wsl2]
memory=10GB  # Limits VM memory in WSL 2GB, also can be set to other values