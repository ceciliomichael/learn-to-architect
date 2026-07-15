# Exercise Solutions: Packages, Modules, and Visibility

`price/price.go`:

```go
// Package price calculates validated monetary totals in integer cents.
package price

import "fmt"

func valid(cents, quantity int) bool { return cents >= 0 && quantity >= 0 }

func Subtotal(cents, quantity int) (int, error) {
	if !valid(cents, quantity) {
		return 0, fmt.Errorf("cents and quantity must be nonnegative")
	}
	return cents * quantity, nil
}
```

`cmd/shop/main.go`:

```go
package main

import (
	"fmt"

	"example.com/course/shop/price"
)

func main() {
	total, err := price.Subtotal(125, 3)
	if err != nil {
		fmt.Println("subtotal failed:", err)
		return
	}
	fmt.Println(total)
}
```

From the root run:

```text
go mod init example.com/course/shop
gofmt -w .
go test ./...
go vet ./...
go mod tidy
go run ./cmd/shop
```

The command depends on `price`; `price` does not import the command, so the dependency direction has no cycle.
