# Exercise Solutions: Variables, Constants, and Basic Types

```go
package main

import "fmt"

func main() {
	title := "Go Foundations"
	lessons := 34
	price := 19.95
	available := true
	var note string
	var archived bool
	const MaxClassSize = 24

	lessons = 35
	fmt.Printf("%s %d %.2f %t\n", title, lessons, price, available)
	fmt.Printf("note=[%s] archived=%t maximum=%d\n", note, archived, MaxClassSize)
}
```

Assigning `"thirty-five"` to `lessons` fails because the name has type `int`. Reassign it with an integer such as `35`.
