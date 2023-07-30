
Дженеріки - штука, яка приїхала в GO в 1.18.

допомагає уникнути дублювання кода за рахунок універсального параметра 

сигнатура - `[<TypeName> <constraint>]`

```go
func MyPrintln[T any](val T) {
	fmt.Println("my println")
	fmt.Println(val)
}
```


--- 
Констрейнти можуть бути 3х видів:

1. вбудовані в го (поки що тільки `comparable`)
2. кастомні
3. golang.org/x/exp/constraints


---

в допомогу дженерікам приїхали ще фічі:
- новий токен `~` [[go generics ~]]
- новий інтерфейс comparable (``==` та `!=`)

---






```go
package main  
  
import (  
"fmt"  
"golang.org/x/exp/constraints"  
)  
  
func main() {  
	// замість  
	fmt.Println(MaxInt(2, 3))  
	fmt.Println(MaxUint(2, 5))  
	  
	// маємо  
	fmt.Println(Max(2, 3))  
	fmt.Println(Max(2.0, 5.0))  
	fmt.Println(Max("test1", "test2"))  
}  
  
func MaxInt(x, y int) int {  
	if x > y {  
		return x  
	}  
	  
	return y  
}  
  
func MaxUint(x, y uint) uint {  
	if x > y {  
		return x  
	}  
	  
	return y  
}  
  
// go get golang.org/x/exp/constraints  
func Max[T constraints.Ordered](x, y T) T {  
	if x > y {  
		return x  
	}  
	  
	return y  
}
```


Класні статті:
- https://benjiv.com/golang-generics-introduction/#type---comparable
- https://pkg.go.dev/golang.org/x/exp/constraints#Integer

Класні відео:
- https://youtu.be/PXsojiyWOXA

Ще приклади дженеріків:
- [[custom generics]]
- [[golangorg constraints]]