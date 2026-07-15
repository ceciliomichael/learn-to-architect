# Exercise Solutions: Use the Go Playground and Install Go

```go
package main

import "fmt"

func main() {
	fmt.Println("Go checks my source.")
	fmt.Println("Go compiles my program.")
	fmt.Println("Then the program runs.")
}
```

After observing the missing-brace error, restore the final `}`. Local commands are:

```text
go run main.go
gofmt -w main.go
go build main.go
```

In PowerShell, run the Windows executable with `.\main.exe`. On macOS or Linux, use `./main`. The exact executable suffix depends on the target operating system.
