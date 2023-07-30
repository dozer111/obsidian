```go
package main  
  
import "fmt"  
  
func main() {  
	DoSth(1)  
	DoSth("two")  
	DoSth(false)  
}  
  
type MyGeneric interface {  
	int | string | bool  
}  
  
func DoSth[T MyGeneric](x T) T {  
	fmt.Printf("%T %v\n", x, x)  
	return x  
}
```