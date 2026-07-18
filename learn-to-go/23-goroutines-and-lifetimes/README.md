# Module 23: Goroutines and Lifetimes

## What you will learn

You will start concurrent functions, wait for completion, and give every goroutine a clear owner and lifetime.

```go
package main

import (
	"fmt"
	"sync"
)

func printLabel(label string, wait *sync.WaitGroup) {
	defer wait.Done()
	fmt.Println(label)
}

func main() {
	var wait sync.WaitGroup
	labels := []string{"one", "two", "three"}
	wait.Add(len(labels))
	for _, label := range labels {
		go printLabel(label, &wait)
	}
	wait.Wait()
}
```

`go` starts a function concurrently and returns immediately. Scheduling and output order are not guaranteed. A command can exit while goroutines remain, so the owner waits for every required task.

Call `Add` before starting workers. Each started worker calls `Done` exactly once, normally through defer. `WaitGroup` coordinates completion; it does not collect results or make shared data safe.

Pass loop values as function arguments so data ownership is obvious. Modern Go gives range variables per-iteration semantics in modules using Go 1.22 or newer, but explicit parameters remain easier to review.

A panic in any goroutine normally terminates the process. Return failures through a designed result mechanism. Do not silently recover inside every worker.

## Check your understanding

You are ready when every goroutine in a drawing has a starter, completion signal, and owner that observes completion.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
