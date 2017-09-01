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
数组之间的赋值是值赋值，即
