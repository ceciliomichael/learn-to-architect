# Exercise Solutions: Pointers, Values, and Mutation

```go
package main

import "fmt"

type Counter struct{ Value int }

func reassignLocal(number int) { number = 99 }

func setNumber(number *int, value int) {
	if number != nil {
		*number = value
	}
}

func reset(flag *bool) {
	if flag != nil {
		*flag = false
	}
}

func incremented(counter Counter) Counter {
	counter.Value++
	return counter
}

func increment(counter *Counter) {
	if counter != nil {
		counter.Value++
	}
}

func main() {
	number := 4
	reassignLocal(number)
	fmt.Println(number)
	setNumber(&number, 8)
	fmt.Println(number)

	active := true
	reset(&active)
	fmt.Println(active)

	original := Counter{Value: 1}
	copy := incremented(original)
	increment(&original)
	fmt.Println(original, copy)
}
```

Returning a changed copy and mutating through a pointer are both valid when their contracts are clear. Choose from meaning and evidence, not a rule that pointers are always faster.
