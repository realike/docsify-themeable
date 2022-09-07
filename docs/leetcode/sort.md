# sort

## 冒选插O(n^2)
```go
slice := []int{10, 9, 1, 3, 2, 1}
```

## 冒泡排序
```go
// 每次沉淀最大数字至最后
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

## 选择排序
```go
func sort(slice []int) {
	var maxIndex int
	for i := 0; i < len(slice)-1; i++ {
		maxIndex = i
		for j := i + 1; j < len(slice); j++ {
			if slice[maxIndex] > slice[j] {
				maxIndex = j
			}
		}

		slice[i], slice[maxIndex] = slice[maxIndex], slice[i]
	}
}
```

## 插入排序
```go
func sort(slice []int) {
    for i := 1; i < len(slice); i++ {
        for j := i; j >= 1 && slice[j-1] > slice[j]; j-- {
            slice[j-1], slice[j] = slice[j], slice[j-1]
        }
    }
}
```

## 希堆快归O(nlogn)

## 快速排序
```go

```
