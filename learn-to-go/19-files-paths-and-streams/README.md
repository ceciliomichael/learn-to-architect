# Module 19: Files, Paths, and Streams

## What you will learn

You will work with local files safely, clean up resources, bound reads, and avoid treating paths as trusted text.

```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	file, err := os.Open("notes.txt")
	if err != nil {
		fmt.Fprintln(os.Stderr, "open notes:", err)
		return
	}
	defer file.Close()

	scanner := bufio.NewScanner(file)
	for scanner.Scan() {
		fmt.Println(scanner.Text())
	}
	if err := scanner.Err(); err != nil {
		fmt.Fprintln(os.Stderr, "read notes:", err)
	}
}
```

Acquire a file, check the error, then register cleanup. A deferred `Close` error matters for writes because buffered filesystem failure can appear during close; handle it when durability matters.

Use `path/filepath` for operating-system paths. `path` is for slash-separated paths such as URLs. Use `os.ReadFile` only when file size is already bounded and acceptable in memory. Stream larger input through `io.Reader` or a scanner with an intentional token limit.

If a user chooses a path under an allowed directory, resolve and verify containment. Extension checks do not provide authorization. Avoid following unexpected links when the threat model includes filesystem attackers.

For important replacement, write a temporary sibling, sync when required by the durability policy, close it, then rename. Exact atomicity and durability differ by filesystem and operating system.

## Check your understanding

You are ready when you can separate path policy, acquisition, streamed work, cleanup, and reporting.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
