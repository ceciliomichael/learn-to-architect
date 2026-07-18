# Module 33: Embedded Files, Build Constraints, and Generation

## What you will learn

You will include verified static resources, select platform code explicitly, and make generation repeatable and reviewable.

`embed` can place compile-time files into a binary:

```go
package message

import _ "embed"

//go:embed default.txt
var defaultMessage string

func Default() string { return defaultMessage }
```

Patterns are evaluated during the build. Missing matches fail the build. Embedded content increases artifact size and can expose anything included, so never embed secrets or private keys.

A build constraint such as `//go:build windows` selects a file for a target. Place it near the file beginning and keep a blank line before `package`. Prefer filename suffixes like `_windows.go` when they express the rule clearly. Test every supported target in CI; your current machine compiles only selected files.

`//go:generate` records an explicit development command. `go generate` is not run by `go build`. Generators execute local programs with developer permissions, so review commands and dependencies. Commit generated output when team policy requires reproducible consumer builds and make drift detectable.

Cross-compile pure Go commands with controlled `GOOS` and `GOARCH`. CGO and external linking add platform toolchain requirements.

## Check your understanding

You are ready when you can identify which input enters an artifact, which files each target selects, and how generated output is reproduced.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
