# Exercise Solutions: Interfaces and Type Switches

```go
package main

import (
	"errors"
	"fmt"
)

type MessageReader interface {
	Next() (string, bool)
	Remaining() int
}

type MemoryMessages struct {
	values []string
	index  int
}

func (messages *MemoryMessages) Next() (string, bool) {
	if messages.index >= len(messages.values) {
		return "", false
	}
	value := messages.values[messages.index]
	messages.index++
	return value, true
}

func (messages *MemoryMessages) Remaining() int { return len(messages.values) - messages.index }

type StockError struct{ Requested, Available int }

func (err StockError) Error() string {
	return fmt.Sprintf("requested %d, available %d", err.Requested, err.Available)
}

func describe(value any) string {
	switch typed := value.(type) {
	case string:
		return "text: " + typed
	case int:
		return fmt.Sprintf("integer: %d", typed)
	default:
		return "unsupported"
	}
}

func main() {
	messages := &MemoryMessages{values: []string{"one", "two"}}
	var reader MessageReader = messages
	fmt.Println(reader.Next())
	fmt.Println(reader.Remaining())

	err := fmt.Errorf("reserve: %w", StockError{Requested: 8, Available: 3})
	var stockErr StockError
	if errors.As(err, &stockErr) {
		fmt.Println(stockErr.Requested, stockErr.Available)
	}
	fmt.Println(describe("ready"), describe(7))
}
```
