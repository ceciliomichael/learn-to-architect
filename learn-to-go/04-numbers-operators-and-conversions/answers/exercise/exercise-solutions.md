# Exercise Solutions: Numbers, Operators, and Conversions

```go
package main

import "fmt"

func main() {
	items := 53
	boxSize := 8
	fmt.Println("boxes:", items/boxSize, "left:", items%boxSize)

	price := 4.25
	quantity := 3
	fmt.Printf("subtotal: %.2f\n", price*float64(quantity))

	seconds := 90
	fmt.Println("minutes:", seconds/60, "seconds:", seconds%60)
	fmt.Println("integer third:", 1/3)
	fmt.Println("float third:", 1.0/3.0)
}
```

The outputs include 6 boxes and 5 leftovers, a subtotal of 12.75, and 1 minute with 30 seconds. Formatting controls text output only. Exact-money domains should use integer minor units or a deliberate decimal representation.
