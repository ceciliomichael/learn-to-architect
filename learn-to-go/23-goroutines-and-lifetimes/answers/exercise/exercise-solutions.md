# Exercise Solutions: Goroutines and Lifetimes

```go
package main

import (
	"fmt"
	"sync"
)

func worker(label string, wait *sync.WaitGroup) {
	defer wait.Done()
	fmt.Println("completed", label)
}

func main() {
	labels := []string{"alpha", "beta", "gamma", "delta"}
	var wait sync.WaitGroup
	wait.Add(len(labels))
	for _, label := range labels {
		go worker(label, &wait)
	}
	wait.Wait()
	fmt.Println("all workers completed")
}
```

The final line always follows all worker completion, but worker order is unspecified. A wait group counts lifecycle events only. Concurrent map writes still need one owner, a channel protocol, or synchronization taught next.
