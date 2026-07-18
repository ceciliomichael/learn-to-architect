# Module 11: Structs and Data Modeling

## What you will learn

You will group named fields into clear domain values without adding behavior prematurely.

```go
package main

import "fmt"

type Product struct {
	ID         int
	Name       string
	PriceCents int
	Active     bool
}

func main() {
	book := Product{ID: 1, Name: "Go Guide", PriceCents: 1800, Active: true}
	fmt.Printf("%+v\n", book)
}
```

A struct has a fixed set of named fields. A keyed literal survives field reordering and is clearer than positional values. Missing fields receive zero values, which may still violate domain rules.

Struct assignment copies the fields. If a field is a slice, map, or pointer, the copied field can still share underlying data. Copy depth must match the ownership contract.

Two struct values are comparable only when every field type is comparable. Do not add fields merely to make one current function convenient. Model one coherent concept.

Tags are string metadata attached to fields. Encoding packages can read them later, but tags do not validate values themselves.

Use small nested structs to express real composition. Avoid enormous records whose fields belong to unrelated responsibilities.

## Check your understanding

You are ready when you can create keyed literals, predict zero fields, and explain shallow sharing inside a copied struct.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
