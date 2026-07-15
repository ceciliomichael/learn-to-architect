# Module 09: Arrays and Slices

## What you will learn

You will store ordered values, understand slice sharing, and copy when independent mutation is required.

## Arrays have fixed length

`[3]int` and `[4]int` are different types. Arrays are values, so assignment copies every element.

```go
package main

import "fmt"

func main() {
	array := [3]string{"red", "green", "blue"}
	slice := array[0:2]
	slice[1] = "yellow"
	fmt.Println(array, slice)
}
```

A slice describes part of an underlying array. It has a length and capacity. Mutating an element changes the shared storage, which is why the array now contains `yellow`.

## Append may reuse or replace storage

`append` returns the resulting slice and must be assigned. If capacity is sufficient it can reuse storage; otherwise it allocates another array. Never rely on append preserving or breaking sharing.

Create independent elements with `slices.Clone` or `copy`:

```go
independent := make([]string, len(slice))
copy(independent, slice)
```

A nil slice and empty non-nil slice both have length zero and can be ranged over or appended to, but serialization may distinguish them. Choose from the boundary contract.

Do not change slice length unpredictably while ranging over it. Build a result slice when filtering.

## Check your understanding

You are ready when you can draw a slice's shared array and decide when a copy is required.
