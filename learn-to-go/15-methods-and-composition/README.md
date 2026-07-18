# Module 15: Methods, Embedding, and Composition

## What you will learn

You will attach behavior to named types, choose receivers deliberately, and compose responsibilities without inheritance.

```go
package main

import "fmt"

type Account struct {
	Owner        string
	BalanceCents int
}

func (account *Account) Deposit(cents int) error {
	if cents <= 0 {
		return fmt.Errorf("deposit must be positive")
	}
	account.BalanceCents += cents
	return nil
}
```

A method is a function with a receiver. Use a pointer receiver when the method mutates the value, when copying is undesirable for a measured reason, or when other methods already use pointers consistently. Value receivers work well for small immutable-style values.

Go can automatically take an address for an addressable value in an ordinary method call. This convenience does not change the method set used for interface satisfaction.

## Embed behavior carefully

Embedding a type promotes selected fields and methods, but it is composition, not subclassing. The outer value does not automatically become substitutable for every conceptual role of the embedded type.

Prefer named fields when the relationship deserves a domain name or when promotion would make the API unclear. Keep invariants behind methods and do not expose mutation merely because a field can be exported.

## Check your understanding

You are ready when you can choose a receiver, protect a state rule, and explain embedding without inheritance language.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
