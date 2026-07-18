# Module 21: Tests with the Testing Package

## What you will learn

You will write isolated tests for ordinary, boundary, and failing behavior using Go's standard tools.

Tests live in files ending `_test.go` and functions named `TestXxx` receive `*testing.T`.

```go
package price

import "testing"

func TestSubtotal(t *testing.T) {
	tests := []struct {
		name     string
		price    int
		quantity int
		want     int
	}{
		{name: "ordinary", price: 125, quantity: 3, want: 375},
		{name: "zero quantity", price: 125, quantity: 0, want: 0},
	}

	for _, test := range tests {
		t.Run(test.name, func(t *testing.T) {
			if got := Subtotal(test.price, test.quantity); got != test.want {
				t.Fatalf("Subtotal() = %d, want %d", got, test.want)
			}
		})
	}
}
```

Table-driven tests keep cases visible. A subtest name identifies a failed rule. Use `t.Helper` in assertion helpers so source locations point to the caller.

Use `t.TempDir` for isolated files and `t.Setenv` for temporary environment configuration. Avoid tests that depend on order, real time, public networks, or shared mutable global state.

Run `go test ./...`. Coverage reports which statements ran, not whether the assertions were meaningful. Combine tests with review, validation, fuzzing, static analysis, and production observation.

## Check your understanding

You are ready when one test can fail without depending on another and its message identifies expected and actual behavior.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
