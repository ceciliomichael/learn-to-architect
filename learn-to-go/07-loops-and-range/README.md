# Module 07: Repeat Work with For and Range

## What you will learn

You will use Go's one loop keyword for counted, conditional, and iterable repetition.

## For has several forms

```go
package main

import "fmt"

func main() {
	for number := 1; number <= 3; number++ {
		fmt.Println(number)
	}

	count := 3
	for count > 0 {
		fmt.Println(count)
		count--
	}
}
```

The first loop has initialization, condition, and progress. The second behaves like a while loop. `for {}` repeats until an explicit exit. Every continuing path needs progress or a deliberate wait.

`break` exits the nearest loop. `continue` begins its next iteration. Use both sparingly so the termination rule remains visible.

## Range visits values

```go
text := "Go\u4e16\u754c"
for byteIndex, character := range text {
	fmt.Printf("%d %c\n", byteIndex, character)
}
```

Ranging over a string decodes UTF-8 runes. The index is the starting byte position, not a character count. Later modules use `range` with slices and maps.

Loop variables declared by `range` are per-iteration variables in modern Go modules using Go 1.22 or newer language semantics. Still pass values explicitly to concurrent work because ownership remains clearer.

## Check your understanding

You are ready when you can show initialization, condition, progress, and termination for each loop.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
