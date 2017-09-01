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
