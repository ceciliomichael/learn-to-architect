# Exercise Solutions: Synchronization and the Race Detector

```go
package main

import (
	"fmt"
	"sync"
)

type Counter struct {
	mu    sync.Mutex
	value int
}

func (counter *Counter) Add(delta int) {
	counter.mu.Lock()
	defer counter.mu.Unlock()
	counter.value += delta
}

func (counter *Counter) Value() int {
	counter.mu.Lock()
	defer counter.mu.Unlock()
	return counter.value
}

func main() {
	var counter Counter
	var wait sync.WaitGroup
	for range 4 {
		wait.Add(1)
		go func() {
			defer wait.Done()
			for range 500 {
				counter.Add(1)
			}
		}()
	}
	wait.Wait()
	fmt.Println(counter.Value())

	results := make(chan int, 3)
	for _, value := range []int{2, 3, 4} {
		go func(number int) { results <- number * number }(value)
	}
	total := 0
	for range 3 {
		total += <-results
	}
	fmt.Println(total)
}
```

The mutex protects every read and write of `value`. The second design gives the main goroutine sole ownership of `total`, so no total lock is needed. Run it with `go run -race main.go`.
