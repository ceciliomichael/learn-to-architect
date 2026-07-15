# Exercise Solutions: Generics

```go
package main

import "fmt"

func Last[T any](values []T) (T, bool) {
	var zero T
	if len(values) == 0 {
		return zero, false
	}
	return values[len(values)-1], true
}

func Contains[T comparable](values []T, wanted T) bool {
	for _, value := range values {
		if value == wanted {
			return true
		}
	}
	return false
}

type Pair[A, B any] struct {
	First  A
	Second B
}

func (pair Pair[A, B]) Reverse() Pair[B, A] {
	return Pair[B, A]{First: pair.Second, Second: pair.First}
}

func main() {
	fmt.Println(Last([]int{2, 4, 6}))
	fmt.Println(Contains([]string{"go", "rust"}, "go"))
	fmt.Println(Pair[string, int]{First: "age", Second: 20}.Reverse())
}
```

The generic algorithms preserve input types without conversion. A one-use wrapper around `fmt.Println` would not gain a useful relationship and should remain concrete or be omitted.
