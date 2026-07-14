# Exercise Solutions: Arrays and Slices

```go
package main

import "fmt"

func main() {
	values := [4]string{"zero", "one", "two", "three"}
	middle := values[1:3]
	middle[0] = "ONE"
	fmt.Println(values)

	tasks := []string{"read"}
	tasks = append(tasks, "practice", "review", "rest")

	independent := make([]string, len(tasks))
	copy(independent, tasks)
	independent[0] = "changed copy"
	fmt.Println(tasks, independent)

	source := []int{-2, 0, 3, 5}
	positive := make([]int, 0, len(source))
	for _, number := range source {
		if number > 0 {
			positive = append(positive, number)
		}
	}
	fmt.Println(source, positive)
}
```

The middle slice changes the array because they share storage. `copy` gives the task elements independent outer storage. The filter preserves the source.
