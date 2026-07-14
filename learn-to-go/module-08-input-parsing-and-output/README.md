# Module 08: Read Input, Parse Text, and Format Output

## What you will learn

You will read local terminal input, parse it deliberately, retry expected mistakes, and format results clearly.

## Interactive input requires local Go

The Playground cannot supply normal interactive input. Run this locally:

```go
package main

import (
	"bufio"
	"fmt"
	"os"
	"strconv"
	"strings"
)

func main() {
	reader := bufio.NewReader(os.Stdin)
	fmt.Print("Age: ")
	text, readErr := reader.ReadString('\n')
	if readErr != nil {
		fmt.Fprintln(os.Stderr, "could not read input")
		return
	}

	age, parseErr := strconv.Atoi(strings.TrimSpace(text))
	if parseErr != nil || age < 0 {
		fmt.Fprintln(os.Stderr, "age must be a nonnegative whole number")
		return
	}
	fmt.Printf("Next year: %d\n", age+1)
}
```

Input arrives as text. `strconv.Atoi` returns both a value and an error. Never use an invalid result silently. This lesson names errors; Module 13 explains error design fully.

For repeated token input, `bufio.Scanner` is convenient. Check `Scan`, validate `Text`, and inspect `scanner.Err()` after the loop. Scanner has a token-size limit, which can be adjusted deliberately for bounded requirements.

Write normal results to standard output and diagnostics to standard error. Do not echo passwords, tokens, or unnecessary personal data.

## Check your understanding

You are ready when you can describe input as untrusted text and separate reading, trimming, parsing, validating, and reporting.
