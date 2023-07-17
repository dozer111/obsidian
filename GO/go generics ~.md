`~` - якщо стоїть перед вбудованим типом - дозволяє використовувати не лише його, а і похідні від нього типи

**BEST PRATICE!** - використовувати ~ для всіх builtin типів [source](https://benjiv.com/golang-generics-introduction/#caveats-when-defining-constraints-with-methods)

тут буде помилка 

"Cannot use MyEnum as the type MyGeneric. Type does not implement constraint 'MyGeneric' because type is not included in type set ('int', 'string', 'bool')"

Якщо ж в інтерфейсі б стояв ~int, то не було б
```go
package main  
  
import "fmt"  
  
type MyEnum int  
  
const (  
	MyVal1 MyEnum = iota  
	MyVal2  
	MyVal3  
	MyVal4  
)  
  
func main() {  
	DoSth(1)  
	DoSth("two")  
	DoSth(false)  
	DoSth(MyVal4)  
}  
  
type MyGeneric interface {  
	int | string | bool  
}  
  
func DoSth[T MyGeneric](x T) T {  
	fmt.Printf("%T %v\n", x, x)  
	return x  
}
```