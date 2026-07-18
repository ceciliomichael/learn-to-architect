# Module 04: Numbers, Operators, and Conversions

## What you will learn

You will calculate with integers and floating-point values, convert explicitly, and avoid assuming decimal floats are exact.

## Numeric operations follow types

```go
package main

import "fmt"

func main() {
	items := 29
	boxSize := 6
	fmt.Println(items/boxSize, items%boxSize)

	price := 12.50
	quantity := 3
	subtotal := price * float64(quantity)
	fmt.Printf("%.2f\n", subtotal)
}
```

Integer division discards the fractional part. `%` returns the remainder. Go does not silently combine `float64` and `int`, so the quantity is converted deliberately.

Common operators include `+`, `-`, `*`, `/`, and `%`. Parentheses make intended grouping clear. Compound assignments such as `total += value` update an existing variable.

## Choose numeric types from the domain

Use `int` for ordinary counts and indexes unless a protocol requires a fixed width. Unsigned types are not a substitute for validation because subtraction can wrap. Check ranges at input boundaries.

Floating-point values are binary approximations. Formatting to two places changes display, not stored accuracy. Store money as integer minor units or use a reviewed decimal package when domain rules require exact decimal arithmetic.

Integer overflow can wrap according to the integer type. Validate before security-sensitive size calculations and conversions.

## Check your understanding

You are ready when you can predict integer division, remainder, and why mixed numeric operations need explicit conversion.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
