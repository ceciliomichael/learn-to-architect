# Module 03: Variables, Constants, and Basic Types

## What you will learn

You will store values in typed variables, use constants, and recognize useful zero values.

## Variables have one static type

```go
package main

import "fmt"

func main() {
	var module int = 3
	title := "Go Foundations"
	var published bool

	fmt.Printf("%s, module %d, published: %t\n", title, module, published)
}
```

`var module int = 3` states the type. `title := "Go Foundations"` lets the compiler infer `string` from the initial value. Short declaration works inside functions and must introduce at least one new name.

A variable can receive another value of its type. It cannot later become an unrelated type.

## Zero values make declarations usable

Without an initializer, numbers begin at zero, booleans at false, and strings at empty text. A zero value is not always valid for the business domain, so validate meaning even when the language value is usable.

## Constants do not change

```go
const TaxRate = 0.08
```

Constants are compile-time values. An untyped numeric constant can adapt when assigned if its value is representable. Use constants for stable facts in the program, not configuration that should change at deployment.

Use descriptive `camelCase` names inside a package. Capitalization also controls visibility, taught in Module 18.

## Check your understanding

You are ready when you can choose `var`, short declaration, or `const` and predict the zero value of a basic type.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
