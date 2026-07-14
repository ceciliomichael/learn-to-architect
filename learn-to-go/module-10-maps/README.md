# Module 10: Maps

## What you will learn

You will model key-value relationships, distinguish missing values, and avoid relying on iteration order.

```go
package main

import "fmt"

func main() {
	scores := map[string]int{"Ava": 91, "Ben": 84}
	scores["Cleo"] = 88

	score, found := scores["Dana"]
	fmt.Println(score, found)
	delete(scores, "Ben")
}
```

Map lookup returns the value type's zero value when a key is absent. The comma-ok form distinguishes an absent key from a present key whose value is zero.

Maps are reference-like descriptors for runtime-managed storage. Assignment does not clone entries. Copy entries deliberately when independent mutation is needed.

The zero value of a map is nil. Reading and deleting are safe, but assigning an entry panics. Create writable maps with a literal or `make`.

Map iteration order is deliberately unspecified and can change. Sort a separate slice of keys when stable display or tests require ordering.

Only comparable types can be keys. Slices, maps, and functions are not comparable. A `map[T]struct{}` can model a set when the zero-size value carries no extra meaning.

## Check your understanding

You are ready when you can use comma-ok, initialize before writing, and make output order deliberate.
