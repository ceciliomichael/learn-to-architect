# Module 17: Generics

## What you will learn

You will preserve type relationships with type parameters and avoid generic abstractions that add no value.

```go
package main

import "fmt"

func First[T any](values []T) (T, bool) {
	var zero T
	if len(values) == 0 {
		return zero, false
	}
	return values[0], true
}

func main() {
	fmt.Println(First([]string{"Go", "Rust"}))
	fmt.Println(First([]int{3, 5}))
}
```

`T` represents one type chosen for a call. The same `T` connects slice elements to the returned value. `any` allows every type but does not permit operations such as ordering.

A constraint describes permitted type arguments and available operations. `comparable` permits equality and map keys. Use type sets when a function genuinely supports a family of underlying types.

Generic named types can store type-related values. Methods on them declare the receiver's type parameters.

Start with concrete code. Use generics when they remove repeated type-safe algorithms or data structures while preserving meaningful relationships. Interfaces remain better for varied runtime behavior.

## Check your understanding

You are ready when you can identify the relationship a type parameter preserves and explain why `any` is not dynamic typing.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
