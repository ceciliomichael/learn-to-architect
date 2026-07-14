# Module 25: Context and Cancellation

## What you will learn

You will propagate cancellation and deadlines through request-scoped call chains without storing optional configuration in context.

```go
package main

import (
	"context"
	"fmt"
	"time"
)

func work(ctx context.Context) error {
	select {
	case <-time.After(50 * time.Millisecond):
		return nil
	case <-ctx.Done():
		return ctx.Err()
	}
}

func main() {
	ctx, cancel := context.WithTimeout(context.Background(), time.Second)
	defer cancel()
	fmt.Println(work(ctx))
}
```

Pass context as the first parameter, normally named `ctx`. Do not store it in a long-lived struct. The caller creates cancellation and always calls the returned cancel function to release timer resources.

Cancellation is cooperative. Functions must observe `Done` or call APIs that do. It does not force arbitrary code to stop. Return `ctx.Err()` or wrap it so callers can recognize deadline and cancellation causes.

Context values are for request-scoped metadata that must cross API boundaries, such as a trace ID. They are not for optional function parameters, dependencies, or secrets. Use private key types to avoid collisions and validate any value before trust.

Derive child contexts from the incoming context so upstream cancellation propagates.

## Check your understanding

You are ready when you can trace who creates, passes, observes, cancels, and releases each context.
