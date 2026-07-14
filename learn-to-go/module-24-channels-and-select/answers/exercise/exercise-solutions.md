# Exercise Solutions: Channels and Select

```go
package main

import (
	"fmt"
	"time"
)

func produce(output chan<- int) {
	defer close(output)
	for number := 1; number <= 5; number++ {
		output <- number
	}
}

func consume(input <-chan int) {
	for value := range input {
		fmt.Println(value)
	}
}

func main() {
	values := make(chan int)
	go produce(values)
	consume(values)

	closed := make(chan string)
	close(closed)
	value, ok := <-closed
	fmt.Printf("value=%q open=%t\n", value, ok)

	result := make(chan string, 1)
	go func() { result <- "ready" }()
	select {
	case value := <-result:
		fmt.Println(value)
	case <-time.After(100 * time.Millisecond):
		fmt.Println("timed out")
	}
}
```

The producer is the only closer. The one-result channel is buffered so its worker can finish even if the timeout wins first.
