`go get golang.org/x/exp/constraints`


основні типи:
- Integer (`Signed | Unsigned`)
	- signed (`~int | ~int8 | ~int16 | ~int32 | ~int64`)
	- unsigned (`~uint | ~uint8 | ~uint16 | ~uint32 | ~uint64 | ~uintptr`)
- Float
- Complex
- Ordered (`Integer | Float | ~string`)