# Exercise Solutions: Booleans, Conditions, and Switch

```go
package main

import "fmt"

func main() {
	score := 82
	if score >= 90 {
		fmt.Println("excellent")
	} else if score >= 75 {
		fmt.Println("good")
	} else if score >= 60 {
		fmt.Println("passing")
	} else {
		fmt.Println("review")
	}

	active := true
	role := "editor"
	if active && (role == "owner" || role == "editor") {
		fmt.Println("allowed")
	}

	denominator := 0
	if denominator != 0 {
		fmt.Println(10 / denominator)
	} else {
		fmt.Println("cannot divide by zero")
	}

	color := "amber"
	switch color {
	case "green":
		fmt.Println("go")
	case "amber":
		fmt.Println("prepare to stop")
	case "red":
		fmt.Println("stop")
	default:
		fmt.Println("unknown signal")
	}

	if length := len("Go"); length == 2 {
		fmt.Println("two bytes")
	}
}
```
