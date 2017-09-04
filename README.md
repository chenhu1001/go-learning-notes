# go-learning-notes
## 1、以下程序的输出结果并分析原因
```
package main

import (
	"fmt"
)

func main()  {
	var fs  = [4]func(){}

	for i := 0; i < 4; i++ {
		defer fmt.Println("defer i = ", i)
		defer func() { fmt.Println("defer_closure i = ", i)}()
		fs[i] = func() {
			fmt.Println("closure i = ", i)
		}
	}

	for _, f := range fs{
		f()
	}
}
```

## 2、Go语言中的字符类型  
Go语言中支持两种字符类型，一个是byte（实际上是uint8的别名）；另一个是rune，代表单个unicode字符。  
byte：int8别称  
rune：int32别称  

## 3、Go字符串中字符的修改

```
var s string  = "hello"
s[0] = 'c'   // 错误的写法
```

正确的写法一：

```
c := []byte(s)
c[0] = 'c'
s2 := string(c)
```

正确的写法二：

```
s = "c" + s[1:]
```

## 4、iota关键字
* 这个关键字在声明enum的时候使用，它默认开始值是0，const中每增加一行加1。
* 每遇到一个const关键字，iota就会重置。
* iota在同一行值相同，也就是说iota的值跟它所在行数相等（从0开始）。

## 5、数组之间的赋值
数组之间的赋值是值赋值，即当把一个数组作为参数传入函数的时候，传入的其实是该数组的副本，而不是它的指针。

## 6、数组声明

```
var arr [10]int
a := [3]int{1, 2, 3}
```

## 7、slice声明

```
var fslice []int

slice := []byte{'a', 'b', 'c', 'd'}

var ar = [10]byte{'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'}

var a, b []byte
a = ar[2:5]
b = ar[3:5]
```

## 8、map声明

```
var num map[string] int
num = make(map[string] int, 100)

num := make(map[string] int, 100)
```

## 9、package别名

```
import (
	io "fmt"   // 使用别名调用包 io.Println("Hello World!")
)

import (
	. "fmt"   // Println("Hello World!")
)
```

## 10、go语言中type的几种使用
* 定义结构体

```
type Person struct {
	name string
	age int
} 
```

* 类型等价定义

```
type name string
var myname name = "tao2s"   // 其实就是字符串类型
```

* 结构体内嵌匿名成员

```
type Person struct {
	string
	age int
}
```

* 定义接口类型

```
type Personer interface {
	Run()
	Name() string
}
```

* 定义函数类型

```
type hander func(name string) int
```

## 11、uintptr类型
uintptr是整型，可以足够保存指针的范围，在32位平台下为4个字节，在64位平台下为8个字节。
