# Module 12: Functions and Multiple Results

## What you will learn

You will create focused functions, return several related values, and pass behavior deliberately.

```go
package main

import "fmt"

func divide(dividend, divisor int) (int, int, bool) {
	if divisor == 0 {
		return 0, 0, false
	}
	return dividend / divisor, dividend % divisor, true
}

func main() {
	quotient, remainder, ok := divide(17, 5)
	fmt.Println(quotient, remainder, ok)
}
```

Adjacent parameters with one type can share its declaration. A function can return multiple values without packing them into a hidden object. Use a boolean only when it clearly means presence or success; richer failures use errors next.

Named result parameters can help short functions document closely related results, but they also create mutable hidden state. Prefer explicit returns when names do not improve clarity.

Variadic parameters such as `func sum(values ...int)` receive a slice. Use them when calls naturally have varying counts, not to avoid designing a real input type.

Functions are values. They can be passed as callbacks or returned as closures. A closure can retain surrounding variables, so mutable captured state needs the same ownership and concurrency care as any other state.

## Check your understanding

You are ready when you can distinguish parameters, arguments, results, and side effects and keep one function focused.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
