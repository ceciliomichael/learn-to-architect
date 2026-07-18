# Module 01: Use the Go Playground and Install Go

## What you will learn

You will run a Go program in a browser, recognize the compiler's job, and use the local toolchain when it is available.

## Start in the browser

Open <https://go.dev/play/>. Replace the example with:

```go
package main

import "fmt"

func main() {
	fmt.Println("I am learning Go.")
}
```

Select **Run**. The Playground compiles the source, runs the result in a restricted environment, and shows standard output. Select **Format** to apply the layout expected by Go tools.

The words `package`, `import`, and `func` will be explained next. For now, notice that punctuation and letter case matter.

## Local Go gives you the full toolchain

After installing from <https://go.dev/dl/>, check it with `go version`. Save the program as `main.go`, then use:

```text
go run main.go
gofmt -w main.go
go build main.go
```

`go run` creates a temporary executable and runs it. `go build` creates an executable you can run again. `gofmt` rewrites layout, not program meaning.

## Compiler errors are useful evidence

Delete the final `}` and run again. The compiler reports where parsing stopped and what it expected. Read the first relevant message, compare that line with the working version, repair one thing, and rerun.

The Playground cannot accept interactive input or freely access files and networks. Later modules clearly mark local-only work.

## Check your understanding

You are ready when you can run, format, deliberately break, repair, and rerun this first program.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
