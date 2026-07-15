# Exercise Solutions: Packages, Main, Imports, and Output

```go
package main

import "fmt"

func main() {
	// The report requires the learner and course on separate lines.
	fmt.Print("Learner: ")
	fmt.Println("Ava")
	fmt.Println("Course: Go Foundations")
}
```

Changing `Println` to `println` after `fmt.` produces an undefined-name error because exported names are case-sensitive. Adding an import that is never referenced produces an imported-and-not-used error. Repair both by using the correct exported name and removing the unnecessary import.
