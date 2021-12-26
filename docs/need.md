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