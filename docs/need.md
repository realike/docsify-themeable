# Need

## 接口与结构体的调用区别
```go
// 调用
type Phone interface {
    call()
	see()
}

type NokiaPhone struct {
}

func (nokiaPhone NokiaPhone) call() {
    fmt.Println("I am Nokia, I can call you!")
}

func (nokiaPhone NokiaPhone) see() {
    fmt.Println("I am Nokia, I can see you!")
}

func main() {
    var phone Phone = new(NokiaPhone) // 本质接口
    phone.call()

	phone1 := new(NokiaPhone) // 本质struct
	phone1.see()
}
```

## 链接文档
```
有哪些值得学习的 Go 语言开源项目？ - 知乎 https://www.zhihu.com/question/20801814
```

```
JWT
单元测试
设计模式
高性能mysql
http/tcp
vue3
golang sync锁和mysql锁(读写锁)

========================

微服务与RPC的关系

++++++++++++++++++++++++
```