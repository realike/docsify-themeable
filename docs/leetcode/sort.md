# sort

## 冒泡 --冒选插
```go
// 每次沉淀最大数字至最后
// slice := []int{10, 9, 1, 3, 2, 1}
func sort(slice []int) {
	for i := 0; i < len(slice)-1; i++ {
		for j := 0; j < len(slice)-1-i; j++ {
			if slice[j] > slice[j+1] {
				slice[j], slice[j+1] = slice[j+1], slice[j]
			}
		}
	}
}
```