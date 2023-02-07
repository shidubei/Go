# Go语言学习

## 程序基本结构和要素

### 包(package)

**包是结构化代码的一种方式：每个程序都由包的概念组成，可以使用自身的包或者从其它包中导入内容。**

**每个Go文件都属于且仅属于一个包，一个包包含很多源文件，因此源文件名称和包名一般不相同**

**每个Go应用包含一个main包，表示可独立执行的程序，包名使用小写字母**

#### 标准库

**Go语言中自带的包被称为标准库，也可以创建自己定义的包。**

**Go语言采用了显示依赖的机制来达到快速编译的目的，如果A.go依赖B.go,B.go依赖C.go，那么编译是，先编译C,B再编译A。编译A时读取的是B而非C**

#### 可见性规则

**当标识符(包括常量、变量、类型、函数、结构等)以一个大写字母开头，使用这种标识符的对象可以被外部包的代码所使用，这被称为导出（java中的public），如果以小写字母开头，则对外是不可见的（java中的private）**

## Go语言基础语法

### 注释

```go
//单行注释，程序不会执行这行语句，写给自己看
/*多行注释，程序不会执行这行语句，写给自己看*/
```

**注释的作用就是增加代码的可读性，能更好的阅读代码**

### 变量

**字面意义，变量即可以变化的量，是可以被赋值的**

```go
package main

func main() {
//定义变量name
    var name string="zhongyi"

}
```

**变量指向的是一块内存空间，可以被赋值覆盖**

#### 变量的定义

**go语言是静态类型语言，就是所有的类型都需要明确的定义。go语言中，声明一个变量常常使用var关键字：**

```go
var name type //即声明、变量名、变量类型
```

变量的命名规则遵循骆驼命名法，即首个单词小写，每个新单词的首字母大写 

**go语言支持批量定义变量，语法如下：**

```go
var (
    addr string
    age int 
)
```

#### 变量的初始化

**即变量的赋值初始化，不赋值的话默认为空，0等。简易的赋值有如下语法：**

```go
name :="zhongyi"
//:=是go语言自动推导变量类型并赋值，在明确变量可以使用，不明确的不能使用
```

#### 变量交换

**go语言中的变量交换十分的简易**

```go
var a int =100
var b int =200
a,b=b,a//这就是go语言中的变量交换
```

#### 匿名变量

**匿名变量的特点是一个下划线“_“,"_"本身是一个特殊的标识符，被称为空白标识符。他可以像其它标识符那样用于变量的声明或赋值（任何类型都可以赋值给他），但任何赋给这个标识符的值都将被抛弃，因此这些值在后续的代码中不能使用，也不可以使用这个标识符作为变量对其他变量进行赋值或运算。使用匿名变量时，只需要在变量声明的地方使用下划线替换即可**

```go
package main
import "fmt"
func test(){
    return 100,200
}
func main(){
    a,_:=test()
    _,b:=test()
   fmt.Println(a,b)
//使用匿名变量可以帮助我们过滤一些不必要的值
}
```

### 常量

**常量是一个简单的标识符，在程序运行的时候，不会被修改的量**

**常量中的数据类型只可以是布尔型、数字型（整数型、浮点数和复数）和字符串型。用const定义**

```go
const URL string ="www.baidu.com"
```

### 常量iota

**iota是go语言中的特殊常量，可以认为是一个可以被编译器修改的常量，iota是go语言的常量计数器**

**iota在const关键字出现时被重置为0（const内部的第一行之前），const每新增一行常量声明将iota计数一次，可以用作枚举值**

```go
const (
    a=iota
    b=iota
    c=iota
)
```

**第一个iota为0，后续自加1**

```go
const (
    a=iota
    b
    c
    d="hh"
    e
    f=100
    g
    h=iota
    i
)
//此时的输出为0,1,2,hh,hh,100,100,7,8，则可以看出，iota是一种特殊的计数器，会自动继承上一个iota之间的距离
//go语言中常量没赋值默认和上一个常量一样，
```

### 布尔类型

**即true和false**

```go
var isFlag bool=true
```

**bool的默认值为false**

**布尔类型的值常用于判断比较的返回值当中，值得一提的是，Go语言中对于值之间得比较有非常严格的限制，只有两个类型相同的值才可以进行比较。如果值的类型是接口，也必须实现相同的接口才能进行比较。如果条件不满足，则必须进行类型强制转换之后才能机械能比较**

### 整型

![](C:\Users\86181\AppData\Roaming\marktext\images\2023-01-15-23-37-44-image.png)

### 浮点型

**float**

### 字符串型

**字符串是UTF-8字符的一个序列(当字符为ASCII码时占用一个字节，其它字符根据需要占用2-4个字节)。深入来讲，字符串是字节的定长数组**

**字符串的内容(纯字节)可以通过标准索引法来获取，在[]中写入索引。但需要注意的是，这种转换方案支队纯ASCII码的字符串有效。**

**获取字符串中某个字节的地址的行为是非法的**

#### strings包

```go
/*前缀和后缀*/
strings.HasPrefix()
strings.HasSuffix()
/*字符串包含关系*/
strings.Contains(s,substr string) bool
/*判断子字符串或字符在父字符串中出现的位置*/
//返回字符串str在s中的索引，以str的第一个字符返回。-1表示不存在
strings.Index(s,str string) int
//返回字符串str在s中最后出现位置的索引（即可能含有多个，但是只返回最后一个）以str的
//的第一个字符返回
strings.LastIndex(s,str string) int
//查询非ASCII码字符在父字符串的位置
strings.IndexRune(s string,r rune) int
/*字符串替换*/
//将字符串str中的前n个字符串old换为new
strings.Replace(str,old,new string,n int) string
/*统计字符串出现次数*/
//统计非重叠次数
strings.Count(s,str string) int
/*重复字符串*/
strings.Repeat(s,count int) string
/*修改大小写*/
strings.ToLower(s) string
strings.ToUpper(s) string
```

### 数据类型转换

**go语言不存在隐式的类型转换，都必须显式**

```go
valueOfTypeB=TypeB (valueOfTypeA)
```

### 函数

#### 函数的声明

```go
//无参无返回值的函数
func f1 (){
}
//有一个参数的函数
func f2 (msg string) {

}
//有两个参数的函数
func f3 (a,b int){

}
//有一个返回值的函数
func f4(a,b int) int {
    c=a+b
    return c
}
//有多个返回值的函数
func f5(x,y string)(string,string){
    return y,x
}
```

#### 函数的执行顺序

**通常来说，main函数是每一个可执行程序所必须包含的。一般来说都是在启动后第一个执行的函数（但是如果存在init()函数，会优先执行init函数）main函数即没有参数，也没有返回类型**

### 可变参数

**当一个函数的参数类型确定，但个数不确定，可以用可变参数...来确定**

```go
func getSum(nums ...int){
    sum:=0
    for i:=0;i<len(nums);i++{
    fmt.Println(nums[i])
    sum+=nums[i]
}
}
func main(){
    getSum(1,2,3,4)
}
```

### Go指针

**go语言中的指针和C语言并无明显不同，其都指向变量的内存地址。当一个指针被定义后没有被分配到任何变量的时候，指针的值为nil，即空指针**

### 切片

**go语言中的切片即动态数组，是对数组的抽象。和数组相比，切片的长度随着切片容量的增大而增大。**

**创建方式如下：**

```go
//声明未定大小的数组来定义切片
var identifier []type
//使用make()函数来创建切片
var slice1 []type=make([]type,len)
或
slice1:=make([]type,len)
//len为切片的初始长度
```

**初始化如下：**

```go
//直接初始化
s:=[]int{1,2,3}
//引用初始化
s:=arr[startIndex:endIndex]
s:=arr[startIndex:]
s:=arr[:endIndex]
```

### Map集合

**map是无序的键值对的集合。通过索引key来快速检索数据。因为Map是无序的，无法决定它的返回顺序。Map是使用hash表来实现的**

### 结构体

### 方法

**方法是一种特殊的函数，是绑定于数据类型的函数。一般的函数隶属于包，通过包调用。但是方法隶属于数据类型，通过数据就可以调用。一般来说，常见的方法绑定于结构体**

**方法的声明如下**

![](C:\Users\86181\AppData\Roaming\marktext\images\2023-02-02-11-02-34-image.png)

**其中，(srv Type)部分被称为方法的receiver，这就是和函数区别的地方。这里的Type可以为值类型，也可以为指针类型**

#### 值类型方法

**当方法不涉及对receiver中的变量值进行修改的时候，选择receiver为值类型。即方法只对值进行打印、输出等不改变值的操作**

#### 指针类型方法

**当方法涉及到对receiver中的变量值进行修改的时候，选择指针类型作为receiver。即方法可以对绑定的数据类型的变量值进行操作**

#### 方法的一些注意事项

**1.方法本身就是函数，由于go语言中没有方法重载这一说法，因此对于同一数据的方法，方法不能重名。但不同数据类的方法可以重名**

### 接口

**go语言中的接口感觉很像面向对象编程的形式。其是一种抽象的数据类型，将一些具有共性的方法抽象出来包含在一起，但并不对这些方法进行具体的实现，所以其它类型实现接口时可以对这些方法进行自定义的扩展**

```go
/*定义接口*/
type interface_name interface {
    method_name1[return_type]
    method_name2[return_type]
    ...
    method_namen[return_type]
}
/*定义结构体*/
type struct_name struct{
    /*variables*/
}
func (struct_name_variable struct) method_name1() [return_type] {

}
...
```

## Go的控制结构

### if-else结构

```go
if 条件判断 {

}esle {

}
```

**需要注意的是，因为Go在编译是会自动在每一行的结尾添加;，因此如果有else判断，else必须和if的右大括号在同一行**

### switch结构

```go
switch var1{
    case val1:
     ...
    case val2:
     ...
    default:
     ...
}
```

### for结构

**Go语言中的循环结构只有for结构，而没有while或者do-while结构**

#### 基本形式

```go
for 初始化语句；条件语句；修饰语句 {

}
```

#### 基于条件判断的形式

```go
for 条件语句 {

}
```

**这种形式的表现类似while循环**

#### 无限循环

```go
for {

}
```

**直接省略掉条件判断的for循环，其默认为条件为true，则会一直循环下去，常用于网络编程中的服务器和客户端之间的等待和接受请求**

#### for-range结构

**Go独有的一种结构，可以用来迭代任何一个集合（数组和map），我理解为键值对匹配，一般形式为**

```go
for ix,val :=range coll{

}
```

**其中ix为索引值，val用于接收索引对应的值的拷贝，一般只具备只读性质，对val的修改不会影响集合中原有的值，但是如果val是指针，那么产生指针的拷贝会对集合中原有的值进行修改**

## Go的错误处理机制

### 自定义错误处理——error

#### error机制

**go语言使用一个error接口来表示错误类型**

```go
type error interface {
    Error() string
}
```

**该接口包含一个返回值为string类型的Error方法,也就是说，当函数或方法需要返回错误的时候，返回的是一个string的值**

****

**error是可以自定义的错误处理，感觉是编程时能够预料到的错误时可以自定义error来进行处理。比如除法中分母为0等等能够预料到的情况。也就是说对于难以预料的错误和异常，error并不能起到很好的处理作用。**

**由于error是一个接口，其方法可以被自定义实现**

**示例如下**

```go
package main

import (
    "fmt"
    "errors"
)
func main(){
    res1,err1:=div(2,1)
    fmt.Println(res1,err1)
    res2,err2:=div(2,0)
    fmt.Println(res2,err2)
}
func div(a,b int) (int,error){
    if b==0{
//error的一种创建形式，error.New
    return 0,error.New("除数不为0")
}
    else {
    return a/b,nil
}
}
```

### 资源清理——defer

**defer关键字的作用是延后执行，被赋予defer关键字的语句只有在程序结束的时候才运行，但语句的参数传递是在正常的位置传递，只有执行的顺序被延后**

**有多个defer存在的时候，defer遵循先进后出的栈原则**

**示例：**

```go
func main() {
    defer fmt.Println(1)
    fmt.Println(2)
    defer fmt.Println(3)
    fmt.Println(4)
    fmt.Println(5)
    defer fmt.Println(6)
}
```

**结果：**

![](C:\Users\86181\AppData\Roaming\marktext\images\2023-02-02-16-23-11-image.png)

**即对需要清理的资源，在其前加上defer关键字，这样资源的清理将会在程序结束时执行值得注意的是，defer后面不能接赋值类型的语句，否则会报错，但可以接方法，判断等语句**

### 运行恐慌——panic

**panic是go语言的内置函数，对于可以预见的错误，我们能通过error来进行处理，但是对于运行时的错误，需要通过panic函数来进行处理**

### 捕获panic——recover

**recover是go语言的内置函数之一。常用于捕获panic函数的相关内容**

## Go的并发处理机制

**并发/并行：多线程程序在单核心的cpu运行，称为并发；多线程程序在多核心的cpu运行，称为并行。并发的实现依赖于时间片的切换处理。**

### 协程（go程）/线程

**协程：独立的栈空间，共享堆空间，调度用户自行控制，轻量级的线程**

### Goroutine

**非常轻量级的实现，单个进程可以实现成千上万的并发任务**

**goroutine使用go关键字进行创建。将go声明放置在需要调用的函数之前，在相同地址空间运行这个函数。执行时候会作为一个独立的并发线程**

```go
/*普通程序*/
package main

import (
    "fmt"
    "time"
)


func test(){
    for i:=0;i<5;i++ {
    fmt.Printf("test()%d\n",i)
    time.Sleep(time.Second)
}
}
func main(){
    test()
     for i:=0;i<5;i++ {
    fmt.Printf("main()%d\n",i)
    time.Sleep(time.Second)
}
}
```

**结果如下：**

![](C:\Users\86181\AppData\Roaming\marktext\images\2023-02-02-14-08-18-image.png)

**将test之前加入go，使之成为并发的协程，实现并发**

```go
/*普通程序*/
package main

import (
    "fmt"
    "time"
)


func test(){
    for i:=0;i<5;i++ {
    fmt.Printf("test()%d\n",i)
    time.Sleep(time.Second)
}
}
func main(){
    go test()
     for i:=0;i<5;i++ {
    fmt.Printf("main()%d\n",i)
    time.Sleep(time.Second)
}
}
```

**结果如下：**

![](C:\Users\86181\AppData\Roaming\marktext\images\2023-02-02-14-10-13-image.png)

**可见并发之后，test函数和main函数在两个协程间独立运行，互不干扰，结果也无序。**

**除此之外，goroutine还有其它的创建方式**

```go
go func(参数){
    函数体
}(参数)
```

### Channel(通道)

**对于并发运行程序，很重要的一点就是程序之间的通信，go语言中采取的是通道机制来进行程序之间的通信**

**利用channel可以在两个或多个goroutine之间传递消息。channel作为类型相关，一个channel只能传递一种类型的值。这个类型在声明channel时指定。channel可以理解为一种队列，遵循先进先出的原则**

```go
//声明
ch1:=make(chan int)//int类型的无缓冲信道
ch2:=make(chan int,2)//int类型的有缓冲信道
ch3:=make(chan *os,3)//文件类型的有缓冲信道
```

**对于通道，其发送接收使用特殊的操作符<-,如ch<-1**

**1.在向数据向通道中进行发送的时候，如果接收方一直都没有接收，发送操作将持续阻塞。**

**2.同样的，在接收数据时，如果接收方接收的时候，通道中没有发送方发送数据，接收方将会发生阻塞，直到发送方发送数据为止。**

```go
/*接收数据的四种写法*/
/*1.阻塞式接收数据*/
data:=<-ch
//持续阻塞直到发送方向通道发送数据
/*2.非阻塞式接收数据*/
data,ok:=<-ch
/*3.接收任意数据，忽略接收的数据*/
//和1一样属于阻塞接受，但并不利用数据
<-ch
//这种表达可以利用来控制程序的运行，实现同步
/*4.循环接收*/
for data:=range ch{
}
```

#### 无缓冲通道

**即在接受前没有能力保存任何值的通道，要求发送方和接收方同时准备好才能完成发送和接收的操作**

#### 有缓冲通道

**即在被接收前能存储一个或多个值的通道。不要求协程之间必须同时完成发送和接收，其阻塞条件和无缓冲通道有不同，当通道满时，发送方阻塞无法发送。当通道空时，接收方阻塞无法接收。**

**接收方和发送方不必在同时准备好发送和接收。且必须限制缓冲大小，若没有大小限制，缓冲区可以无限扩充的话，那么当发送方的发送速率大于接收方的接收速率时会出现一直扩充的情况。**

#### Channel超时处理机制——select

**在go中，select用于监听和channel相关的IO操作,当IO操作发生时，触发相应的case动作，可以实现main主线程和go程之间的互动**

**select语句和switch语句很相似，二者都是和case相绑定，不同的是switch中对case没有限制且是顺序执行。**

**而select中对case的限制为必须为IO操作，且select中的case语句为随机执行，即当多个case满足的时候，随机执行其中一个。同样的，select要求default语句的存在，否则当所有case都不满足的时候，select语句会进入死锁。**

**利用select语句的default来进行超时处理**
