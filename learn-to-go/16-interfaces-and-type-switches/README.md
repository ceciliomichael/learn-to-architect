# Module 16: Interfaces and Type Switches

## What you will learn

You will describe required behavior with small interfaces, understand implicit satisfaction, and inspect dynamic values safely.

```go
package main

import "fmt"

type Writer interface {
	Write(string) error
}

type MemoryWriter struct{ Messages []string }

func (writer *MemoryWriter) Write(text string) error {
	writer.Messages = append(writer.Messages, text)
	return nil
}

func Save(writer Writer, text string) error { return writer.Write(text) }

func main() {
	memory := &MemoryWriter{}
	if err := Save(memory, "ready"); err != nil {
		fmt.Println(err)
	}
	fmt.Println(memory.Messages)
}
```

A type satisfies an interface by having its methods. It does not declare the relationship. Define small interfaces where behavior is consumed, not beside every implementation by habit.

An interface value contains a dynamic type and dynamic value. An interface holding a typed nil pointer is not itself nil. Avoid returning typed nil values as errors or interface results.

Type assertions use `value, ok := input.(Concrete)`. Type switches handle several expected dynamic types. Do not use them to replace a clearer polymorphic method.

Custom error types implement the built-in `error` interface with `Error() string`. Use `errors.As` when callers need structured fields through a wrapping chain.

## Check your understanding

You are ready when you can place a small interface at its consumer and explain the typed-nil trap.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
