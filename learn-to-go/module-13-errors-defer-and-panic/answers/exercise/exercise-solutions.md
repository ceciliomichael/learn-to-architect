# Exercise Solutions: Errors, Defer, Panic, and Recovery Boundaries

```go
package main

import (
	"errors"
	"fmt"
)

var ErrInvalidQuantity = errors.New("quantity must be positive")
var ErrInsufficientStock = errors.New("insufficient stock")

func validateQuantity(quantity int) error {
	if quantity <= 0 {
		return ErrInvalidQuantity
	}
	return nil
}

func reserve(requested, available int) error {
	if err := validateQuantity(requested); err != nil {
		return fmt.Errorf("reserve stock: %w", err)
	}
	if requested > available {
		return fmt.Errorf(
			"%w: requested %d, available %d",
			ErrInsufficientStock,
			requested,
			available,
		)
	}
	return nil
}

func work() {
	fmt.Println("acquired practice resource")
	defer fmt.Println("released practice resource")
	fmt.Println("working")
}

func main() {
	err := reserve(0, 3)
	fmt.Println(errors.Is(err, ErrInvalidQuantity), err)

	err = reserve(8, 3)
	fmt.Println(errors.Is(err, ErrInsufficientStock), err)
	work()
}
```

Validation returns ordinary errors because the caller can report and correct the input. Panic would bypass that normal recovery path.
