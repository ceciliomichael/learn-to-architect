# Module 26: Synchronization and the Race Detector

## What you will learn

You will protect shared invariants, prefer clear ownership, and use the race detector as runtime evidence.

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
	counter.Add(2)
	fmt.Println(counter.Value())
}
```

A mutex protects an invariant, not merely a line. Keep it private with the data, hold it for the shortest clear operation, and never copy a used mutex. Establish one lock order when several locks are unavoidable.

`RWMutex` helps only for measured read-heavy workloads and adds complexity. `sync.Once` runs initialization once. Atomics are appropriate for carefully defined single-word state, not compound business rules.

Prefer one owner or message passing when it makes mutation simpler. Use `go test -race ./...` and run realistic paths. The race detector finds only races exercised during that run and does not prove higher-level correctness or deadlock freedom.

## Check your understanding

You are ready when you can name the invariant protected by every lock and demonstrate the relevant path under the race detector.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
