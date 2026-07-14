# Exercise Solutions: Functions and Multiple Results

```go
package main

import "fmt"

func area(width, height float64) float64 { return width * height }

func formatPrice(cents int) string { return fmt.Sprintf("%d.%02d", cents/100, cents%100) }

func bounds(values []int) (int, int, bool) {
	if len(values) == 0 {
		return 0, 0, false
	}
	minimum, maximum := values[0], values[0]
	for _, value := range values[1:] {
		if value < minimum {
			minimum = value
		}
		if value > maximum {
			maximum = value
		}
	}
	return minimum, maximum, true
}

func sum(values ...int) int {
	total := 0
	for _, value := range values {
		total += value
	}
	return total
}

func transform(values []int, operation func(int) int) []int {
	result := make([]int, len(values))
	for index, value := range values {
		result[index] = operation(value)
	}
	return result
}

func prefixer(prefix string) func(string) string {
	return func(text string) string { return prefix + text }
}

func main() {
	fmt.Println(area(3, 4), formatPrice(1250))
	fmt.Println(bounds([]int{8, 2, 11}))
	fmt.Println(sum(2, 3, 4))
	fmt.Println(transform([]int{1, 2}, func(value int) int { return value * 2 }))
	fmt.Println(prefixer("Status: ")("ready"))
}
```
