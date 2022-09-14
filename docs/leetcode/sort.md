# sort

## 冒选插O(n^2)
```go
slice := []int{10, 9, 1, -1,3, 2, 1}
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

## ref
```
https://leetcode.cn/problems/sort-an-array/solution/shi-da-pai-xu-suan-fa-golangshi-xian-by-8p1bl/
https://leetcode.cn/problems/sort-an-array/solution/golang-by-xilepeng-2/
```