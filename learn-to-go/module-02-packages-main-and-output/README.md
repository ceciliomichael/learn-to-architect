# Module 02: Packages, Main, Imports, and Output

## What you will learn

You will identify a runnable Go program, import a standard package, print values, and understand why unused names stop compilation.

## A command starts in package main

```go
package main

import "fmt"

func main() {
	fmt.Println("Ready")
	fmt.Print("Go ")
	fmt.Print("program\n")
}
```

Every Go source file begins with a package declaration. An executable command uses `package main` and provides `func main()`. The runtime calls that function as the entry point.

`import "fmt"` makes the standard formatting package available. `fmt.Println` adds spaces between separate arguments and ends the line. `fmt.Print` prints exactly what you request.

## Names and letter case matter

The capital `P` in `Println` means the name is exported by package `fmt`. `fmt.println` does not exist. Go uses capitalization as part of its visibility rules.

Go rejects unused imports and local variables. This keeps accidental clutter out of finished code. Remove unused work instead of hiding it with the blank identifier during ordinary learning.

## Comments explain intent

Use `//` for a line comment. Use comments to explain a reason, constraint, or surprising rule, not to repeat obvious syntax.

```go
package main

import "fmt"

func main() {
	// Keep this greeting stable because another lesson compares its output.
	fmt.Println("Welcome to Go")
}
```

## Check your understanding

You are ready when you can point to the package, import, entry function, qualified function name, statement endings, and output.
