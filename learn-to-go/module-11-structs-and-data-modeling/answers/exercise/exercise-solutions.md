# Exercise Solutions: Structs and Data Modeling

```go
package main

import "fmt"

type Book struct {
	ID         int
	Title      string
	PriceCents int
	Available  bool
	Tags       []string
}

func main() {
	first := Book{ID: 1, Title: "Clear Go", PriceCents: 1500, Available: true, Tags: []string{"go"}}
	second := Book{ID: 2, Title: "Safe Services", PriceCents: 2100}
	fmt.Println(first.Title, second.Title)

	var empty Book
	fmt.Printf("%+v\n", empty)

	shared := first
	shared.Tags[0] = "shared"
	fmt.Println(first.Tags)

	independent := first
	independent.Tags = append([]string(nil), first.Tags...)
	independent.Tags[0] = "independent"
	fmt.Println(first.Tags, independent.Tags)
}
```

The struct fields are copied, but the first copied slice still names shared storage. Copying its elements creates the intended independent outer data.
