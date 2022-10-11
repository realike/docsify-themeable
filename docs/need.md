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

## 快速排序
```go
// slice := []int{10, 9, 1, -1, 3, 2, 1}
// quickSort(slice, 0, len(slice)-1)
func quickSort(slice []int, low int, high int) {
	if low > high {
		return
	}

	pivot := slice[low]
	i := low
	j := high
	for i < j {
		// 从 j 往前遍历，找到第一个比基数小的数(中断for)，记录其下标
		for i < j && slice[j] >= pivot {
			j--
		}
		// 从 i 开始，遇到比基数大的数，记录其下标
		for i < j && slice[i] <= pivot {
			i++
		}
		slice[i], slice[j] = slice[j], slice[i]
	}
	//基准元素与右哨兵交换	
	slice[low], slice[j] = slice[j], slice[low]	

	quickSort(slice, low, j-1)
	quickSort(slice, j+1, high)
}
```