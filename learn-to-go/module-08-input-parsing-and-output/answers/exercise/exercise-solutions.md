# Exercise Solutions: Read Input, Parse Text, and Format Output

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
	scanner := bufio.NewScanner(os.Stdin)

	fmt.Print("Name: ")
	if !scanner.Scan() {
		fmt.Fprintln(os.Stderr, "name input ended")
		return
	}
	name := strings.TrimSpace(scanner.Text())
	if name == "" {
		fmt.Fprintln(os.Stderr, "name is required")
		return
	}

	quantity := -1
	for quantity < 0 {
		fmt.Print("Nonnegative quantity: ")
		if !scanner.Scan() {
			fmt.Fprintln(os.Stderr, "quantity input ended")
			return
		}
		parsed, err := strconv.Atoi(strings.TrimSpace(scanner.Text()))
		if err != nil || parsed < 0 {
			fmt.Fprintln(os.Stderr, "use a nonnegative whole number")
			continue
		}
		quantity = parsed
	}

	if err := scanner.Err(); err != nil {
		fmt.Fprintln(os.Stderr, "input failed")
		return
	}
	fmt.Printf("%s selected %d items\n", name, quantity)
}
```

The loop assigns `quantity` only after both parsing and range validation succeed. End-of-input and scanner failures are reported separately from invalid user text.
