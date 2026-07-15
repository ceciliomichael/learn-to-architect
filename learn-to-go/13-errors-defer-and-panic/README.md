# Module 13: Errors, Defer, Panic, and Recovery Boundaries

## What you will learn

You will represent expected failure with error values, add context without losing causes, and reserve panic recovery for narrow boundaries.

```go
package main

import (
	"errors"
	"fmt"
)

var ErrInvalidQuantity = errors.New("quantity must be positive")

func subtotal(priceCents, quantity int) (int, error) {
	if quantity <= 0 {
		return 0, ErrInvalidQuantity
	}
	return priceCents * quantity, nil
}

func main() {
	total, err := subtotal(125, 0)
	if err != nil {
		fmt.Println("could not calculate subtotal:", err)
		return
	}
	fmt.Println(total)
}
```

An error is an ordinary value. Check it close to the operation unless the function's job is to return it. Wrap useful context with `fmt.Errorf("load settings: %w", err)` and inspect a sentinel chain with `errors.Is`. Module 16 introduces `errors.As` after custom error types and interfaces. Do not compare error text.

`defer` schedules a call for the surrounding function's return. Deferred calls run in last-in, first-out order and are useful for cleanup immediately after successful acquisition.

Panic indicates that ordinary continuation is impossible, commonly because of a programmer invariant or unrecoverable initialization. It is not a normal validation result. Recover only at a boundary that can restore a valid state, report safely, and stop or continue by documented policy.

## Check your understanding

You are ready when you can return an error, wrap its cause, and explain why recovery is not general error handling.
