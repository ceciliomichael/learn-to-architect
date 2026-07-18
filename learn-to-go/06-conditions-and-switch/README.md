# Module 06: Booleans, Conditions, and Switch

## What you will learn

You will form boolean rules and choose one clear program path.

## Conditions use bool

```go
package main

import "fmt"

func main() {
	score := 82

	if score >= 90 {
		fmt.Println("excellent")
	} else if score >= 75 {
		fmt.Println("good")
	} else {
		fmt.Println("keep practicing")
	}
}
```

Go requires a boolean condition. It does not automatically treat numbers or strings as true or false. Comparisons use `==`, `!=`, `<`, `<=`, `>`, and `>=`. Combine rules with `&&`, `||`, and `!`.

Braces are required. The first true branch runs, so order specific boundaries before broader ones.

## Short setup can belong to an if

```go
if length := len("Go"); length == 2 {
	fmt.Println("two bytes")
}
```

`length` exists only in the `if` and its related branches. Use this when the value has no meaning afterward.

## Switch expresses alternatives

```go
day := "Monday"
switch day {
case "Saturday", "Sunday":
	fmt.Println("weekend")
default:
	fmt.Println("weekday")
}
```

Go cases do not fall through by default. A switch without an expression can replace a long boolean chain. Keep business rules explicit and test their boundaries.

## Check your understanding

You are ready when you can order branches correctly and choose a readable `if` or `switch`.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
