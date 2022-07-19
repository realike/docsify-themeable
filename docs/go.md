# Go-p

## new and make
```
在golang中,make和new都是分配内存的，但是它们之间还是有些区别的，只有理解了它们之间的不同，才能在合适的场合使用。

简单来说,new只是分配内存，不初始化内存； 而make即分配又初始化内存。所谓的初始化就是给类型赋初值，比如字符为空，整型为0, 逻辑值为false等。

new
先看下new函数的定义

// The new built-in function allocates memory. The first argument is a type,
// not a value, and the value returned is a pointer to a newly
// allocated zero value of that type.
func new(Type) *Type
可以看出，它的参数是一个类型，返回值为指向该类型内存地址的指针，同时会把分配的内存置为零，也就是类型的零值, 即字符为空，整型为0, 逻辑值为false

看几个new的示例

   type P struct{
        Name string
        Age int
    }
    var a *[2]int
    var s *string
    var b *bool
    var i *int
    var ps *P
​
    a = new([2]int)
    s = new(string)
    b = new(bool)
    i = new(int)
    ps = new(P) //结构
​
    fmt.Println(a, " ", *a)
    fmt.Println(s,  " ",*s)
    fmt.Println(b,  " ",*b)
    fmt.Println(i,  " ",*i)
    fmt.Println(ps, " ", *ps)
输出结果如下

&[0 0]   [0 0]
0xc00000e1e0   
0xc00001a07a   false
0xc00001a090   0
&{ 0}   { 0}
上面示例是基本的类型，再看下slice, map,chan这些用new咋操作

    map操作
    var mp *map[string]string
    mp = new(map[string]string)
    //*mp = make(map[string]string)  //这行注掉会panic "panic: assignment to entry in nil map""
    (*mp)["name"] = "lc"
    fmt.Println((*mp)["name"])
    
    slice操作
    var ms *[]string
    ms = new([]string)
    //*ms = make([]string,5) //这行注掉会pance "panic: runtime error: index out of range"
    (*ms)[0] = "lc"
    fmt.Println((*ms)[0])
    
上面可以看出，silce、map、channel等类型属于引用类型，引用类型初始化为nil，nil是不能直接赋值的，也不能用new分配内存，还需要使用make来分配。

make
看下make的函数声明

/ The make built-in function allocates and initializes an object of type
// slice, map, or chan (only). Like new, the first argument is a type, not a
// value. Unlike new, make's return type is the same as the type of its
// argument, not a pointer to it. The specification of the result depends on
// the type:
//  Slice: The size specifies the length. The capacity of the slice is
//  equal to its length. A second integer argument may be provided to
//  specify a different capacity; it must be no smaller than the
//  length. For example, make([]int, 0, 10) allocates an underlying array
//  of size 10 and returns a slice of length 0 and capacity 10 that is
//  backed by this underlying array.
//  Map: An empty map is allocated with enough space to hold the
//  specified number of elements. The size may be omitted, in which case
//  a small starting size is allocated.
//  Channel: The channel's buffer is initialized with the specified
//  buffer capacity. If zero, or the size is omitted, the channel is
//  unbuffered.
func make(t Type, size ...IntegerType) Type
可以看出，它返回的就是类型本身，而不是指针类型，因为make只能给slice,map,channel等初始化内存，它们返回的就是引用类型，那么就没必要返回指针了

看下make的一些示例

    mm :=make(map[string]string)
    mm["name"] = "lc"
    fmt.Println(mm["name"])
​
    mss :=make([]int,2)
    mss[0] = 100
    fmt.Println(mss[0])
​
    ch :=make(chan int,1)
    ch <-100
​
    fmt.Println(<-ch)
小结
make 仅用来分配及初始化类型为 slice、map、chan 的数据。new 可分配任意类型的数据. new 分配返回的是指针，即类型 *Type。make 返回引用，即 Type. new 分配的空间被清零, make 分配空间后，会进行初始化.
ref：https://zhuanlan.zhihu.com/p/97854299

ref: https://studygolang.com/articles/29675
golang的值类型，指针类型和引用类型&值传递&指针传递

一，变量类型
变量分为值类型，指针类型和引用类型。
以如下变量定义和赋值语句为例：

package main

import(
    "fmt"
)

func main(){

    var a int = 1
    p := &a
    fmt.Printf("%v\n", a)
    fmt.Printf("%p\n", &a)
    fmt.Printf("%p\n", p)
    fmt.Printf("%p\n", &p)
}
output:

1
0xc000092000
0xc000092000
0xc00008c010

值类型变量和引用类型变量
值类型变量a，值为1，存储变量a的内存地址为0xc000092000
指针类型 &a，某个变量的内存地址，即a的地址0xc000092000。
引用类型p，某个变量的地址的别名。
值为某个变量的内存地址（p的值为变量a的内存地址0xc000092000）
其本身作为一个变量也有自己的存储内存地址0xc00008c010。
在golang中故意淡化了指针的概念，我们只需要关注值类型和引用类型就可以。你在官方介绍中也很少看到指针类型这一概念。

二，golang中的值类型变量和引用类型变量
值类型变量：除开slice，map，channel类型之外的变量都是值类型
引用类型变量：slice，map，channel这三种
三，值类型和引用类型的区别
我们以值类型struct和引用类型map的区别在哪里。
首先定义两种类型的结构及变量：

type Student1 struct{
    Age int32
    Name string
}
type Student2 map[string]int

func main(){
    var s1 Student1
    var s2 Student2
}
1，零值不同
指针类型的变量，零值都是nil。
值类型的变量，零值是其所在类型的零值。
int32类型的零值是0
string类型的零值是""
bool类型的零值是false
符合结构struct类型的零值是其每个成员的零值的组合
fmt.Println(s1) //{0 }
fmt.Println(s2) //map[] 
fmt.Println(s1 == nil) //panic,提示cannot convert nil to type Student1
fmt.Println(s2 == nil) //true
发现map的零值是nil，struct的零值是Student1{0, ""},不是nil，而且struct类型和nil是两种不同的类型，不能比较。

2，变量申明后是否需要初始化才能使用
指针类型的变量，需要初始化才能使用。(slice是一个特例，slice的零值是nil，但是可以直接append)
值类型的变量，不用初始化，可以直接使用
s1.Name = "minping"
s1.Age = 30
fmt.Println(s1) //{30 minping}

s2["minping"] = 30 // panic: assignment to entry in nil map
fmt.Println(s2)
发现struct声明后可以直接使用直接赋值，但是map就不行，赋值的时候提示我们nil map不能赋值，需要先初始化。

3，初始化方法不同
值类型的变量，其实不需要初始化就可以使用。如果有良好的代码习惯，使用前进行初始化也是非常提倡的。
基本类型的初始化非常简单:
var i int; i = 1;
var b bool; b = true
var s string; s = ""
符合类型struct的初始化有两种:
s1 = Student1{}
s1 = new(Student1)
s1 := Student1{} //{0 }

s1 := new(Student1) //&{0 }
引用类型的变量，初始化方式也不一样：
slice类型，用make，new，{}都可以
map类型，用make，new，{}都可以
channel类型，只能用make活着new初始化
//map可以用{}，make，new三种方式初始化
s2 := Student2{} //map[]
s2 := make(Student2) //map[]
s2 := new(Student2) //&map[]

//slice可以用{},make,new,但是make的时候需要带len参数
type S3 []string
s3 := S3{} //[]
s3 := new(S3) //&[]
s3 := make(S3, 10) //[         ]

//channel只能用make或者new
type Student4 chan string
s4 := new(S4) //0xc000096000
s4 := make(S4) //0xc000082008
s4 := S4{} //编译器报错：invalid type for composite literal: Student4
四，make和new的区别
从上面初始化时用make和new的结果就可以看出来：

make返回的是对象。
对值类型对象的更改，不会影响原始对象的值
对引用类型对象的更改，会影响原始对象的值
new返回的是对象的指针，对指针所在对象的更改，会影响指针指向的原始对象的值。
五，golang没有引用传递，都是值传递
如果函数形参是值类型，则会对值类型做一份拷贝作为函数形参。在函数内对形参变量做的修改，不会影响函数外的那个被传入的变量。
如果函数形参是引用类型，则会对引用类型变量做一次拷贝。但是拷贝得到的引用类型变量的值，和被传入调用函数的原始引用类型变量的值，是一样的，即指向的是同一个变量的地址(参考前面值类型变量和引用类型变量图)。所以在函数里面的修改，会影响原始引用变量指向的变量的值。
7 type Student struct{
8
9     Age int
10 }
11
12 func main(){
13
14     s := Student{30}
15     modify1(s)
16     fmt.Println(s) //{30}
17
18     modify2(&s)
19     fmt.Println(s) //{32}
20 }
21
22 func modify1(s Student){
23     s.Age = 31
24 }
25
26 func modify2(s *Student){
27     s.Age = 32
28 }
```