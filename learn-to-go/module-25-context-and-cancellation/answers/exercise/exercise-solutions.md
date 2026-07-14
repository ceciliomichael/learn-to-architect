# Exercise Solutions: Context and Cancellation

```go
package main

import (
	"context"
	"errors"
	"fmt"
	"time"
)

func step(ctx context.Context, duration time.Duration) error {
	select {
	case <-time.After(duration):
		return nil
	case <-ctx.Done():
		return fmt.Errorf("step stopped: %w", ctx.Err())
	}
}

func operation(ctx context.Context, duration time.Duration) error {
	return step(ctx, duration)
}

func run(timeout, duration time.Duration) error {
	ctx, cancel := context.WithTimeout(context.Background(), timeout)
	defer cancel()
	return operation(ctx, duration)
}

func main() {
	fmt.Println("success:", run(time.Second, 10*time.Millisecond))
	err := run(10*time.Millisecond, time.Second)
	fmt.Println("deadline:", errors.Is(err, context.DeadlineExceeded))
}
```

A retry count or output format should be an explicit typed parameter or configuration field. Hiding it in context makes the function contract unclear.
